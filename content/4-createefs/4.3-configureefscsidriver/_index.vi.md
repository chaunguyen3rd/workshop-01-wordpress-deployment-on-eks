---
title: "Cấu hình EFS CSI driver"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 4.3 </b> "
---

Ở bước này, chúng ta sẽ cấu hình EFS CSI driver của chúng ta.

#### Cài đặt **helm**

**Helm** là trình quản lý gói cho Kubernetes giúp đơn giản hóa quá trình triển khai và quản lý các ứng dụng trong cụm Kubernetes. Nó sử dụng "biểu đồ", là các mẫu được cấu hình sẵn để xác định cấu trúc, sự phụ thuộc và các tùy chọn cấu hình của ứng dụng hoặc dịch vụ.

1. Mở terminal của bạn.
   ```
     ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
   ```

- Thay thế the `18.206.88.146` với địa chỉ public IP của máy EC2 của bạn.
- Thay đổi `~/.ssh/labBastionHostSSHKey01.pem` thành đường dẫn của Key pair bạn đã tải về khi tạo ra máy chủ EC2.
- Sau khi đăng nhập thành công vào EC2, chuyển sang sudo user với câu lệnh `sudo su`.

2. Cài đặt **helm**

- Chạy đoạn code này.
  ```
  curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
  sudo apt-get install apt-transport-https --yes
  echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
  sudo apt-get update
  sudo apt-get install helm
  ```
- Kiểm tra việc cài đặt thành công với câu lệnh `helm version`.
  ```
  root@ip-10-0-1-234:~# helm version
  version.BuildInfo{Version:"v3.16.1", GitCommit:"5a5449dc42be07001fd5771d56429132984ab3ab", GitTreeState:"clean", GoVersion:"go1.22.7"}
  root@ip-10-0-1-234:~#
  ```

#### Cấu hình EFS CSI driver

1. Tạo tài khoản dịch vụ **efs-csi-controller-sa**.

- Lưu lại file **aws-efs-csi-driver-sa.yaml**.
  - Thay đổi `arn:aws:iam::017820706022:role/labEKSEFSCSIDriverRole` thành giá trị **labEKSEFSCSIDriverRole**'s ARN.
  ```
  # aws-efs-csi-driver-sa.yaml
  apiVersion: v1
  kind: ServiceAccount
  metadata:
    labels:
      app.kubernetes.io/name: aws-efs-csi-driver
    name: efs-csi-controller-sa
    namespace: kube-system
    annotations:
      eks.amazonaws.com/role-arn: arn:aws:iam::017820706022:role/labEKSEFSCSIDriverRole
  ```
- Chạy `kubectl apply -f aws-efs-csi-driver-sa.yaml`.
  ```
  root@ip-10-0-1-234:~# kubectl get -n kube-system sa | grep efs-csi-controller-sa
  efs-csi-controller-sa                         0         106s
  ```

2. Cài đặt driver using **Helm**

- Thêm Helm repo: `helm repo add aws-efs-csi-driver https://kubernetes-sigs.github.io/aws-efs-csi-driver/`.
- Cập nhật repo: `helm repo update aws-efs-csi-driver`
- Cài đặt một phiên bản của driver bằng cách sử dụng biểu đồ **Helm**.
  ```
  helm upgrade --install aws-efs-csi-driver \
    --namespace kube-system \
    --set controller.serviceAccount.create=false \
    --set controller.serviceAccount.name=efs-csi-controller-sa \
    aws-efs-csi-driver/aws-efs-csi-driver
  ```
- Kiểm tra việc cài đặt thành công.

  ```
  root@ip-10-0-1-234:~# helm repo add aws-efs-csi-driver https://kubernetes-sigs.github.io/aws-efs-csi-driver/
  "aws-efs-csi-driver" has been added to your repositories
  root@ip-10-0-1-234:~# helm repo update aws-efs-csi-driver
  Hang tight while we grab the latest from your chart repositories...
  ...Successfully got an update from the "aws-efs-csi-driver" chart repository
  Update Complete. ⎈Happy Helming!⎈
  root@ip-10-0-1-234:~# helm upgrade --install aws-efs-csi-driver \
    --namespace kube-system \
    --set controller.serviceAccount.create=false \
    --set controller.serviceAccount.name=efs-csi-controller-sa \
    aws-efs-csi-driver/aws-efs-csi-driver
  Release "aws-efs-csi-driver" does not exist. Installing it now.
  NAME: aws-efs-csi-driver
  LAST DEPLOYED: Fri Sep 20 13:51:50 2024
  NAMESPACE: kube-system
  STATUS: deployed
  REVISION: 1
  TEST SUITE: None
  NOTES:
  To verify that aws-efs-csi-driver has started, run:

      kubectl get pod -n kube-system -l "app.kubernetes.io/name=aws-efs-csi-driver,app.kubernetes.io/instance=aws-efs-csi-driver"
  root@ip-10-0-1-234:~# kubectl get pod -n kube-system -l "app.kubernetes.io/name=aws-efs-csi-driver,app.kubernetes.io/instance=aws-efs-csi-driver"
  NAME                                 READY   STATUS    RESTARTS   AGE
  efs-csi-controller-5864df9cf-7klcl   3/3     Running   0          16s
  efs-csi-controller-5864df9cf-hslwm   3/3     Running   0          16s
  efs-csi-node-nms8t                   3/3     Running   0          17s
  efs-csi-node-q5tkf                   3/3     Running   0          17s
  root@ip-10-0-1-234:~#
  ```

#### Tạo Dynamic Provisioning StorageClass

1. Đi đến [EFS service management console](https://console.aws.amazon.com/efs/home)

- Bấm **File systems**.
- Sao chép **fs-0003fc3d543db9be6**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/4.configure/ws01-configure13.png)

2. Tạo **StorageClass**.

- Quay lại terminal của bạn, Lưu lại manifest **StorageClass**.
  ```
  # efs-sc.yaml
  kind: StorageClass
  apiVersion: storage.k8s.io/v1
  metadata:
    name: efs-sc
  provisioner: efs.csi.aws.com
  parameters:
    provisioningMode: efs-ap
    fileSystemId: fs-92107410
    directoryPerms: "700"
    gidRangeStart: "1000" # optional
    gidRangeEnd: "2000" # optional
    basePath: "/dynamic_provisioning" # optional
    subPathPattern: "${.PVC.namespace}/${.PVC.name}" # optional
    ensureUniqueDirectory: "true" # optional
    reuseAccessPoint: "false" # optional
  ```
- Thay thế `fileSystemId: fs-92107410` thành FileSystemID của bạn đã tạo ra ở bước trước.
- Chạy `kubectl apply -f efs-sc.yaml`
- Kiểm tra việc cài đặt thành công.
  ```
  root@ip-10-0-1-234:~# kubectl apply -f efs-sc.yaml
  storageclass.storage.k8s.io/efs-sc created
  root@ip-10-0-1-234:~# kubectl get storageclass
  NAME     PROVISIONER             RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
  efs-sc   efs.csi.aws.com         Delete          Immediate              false                  17s
  gp2      kubernetes.io/aws-ebs   Delete          WaitForFirstConsumer   false                  3d20h
  ```

Tiếp theo, chúng ta sẽ cấu hình **labNodeGroupsRole**.
