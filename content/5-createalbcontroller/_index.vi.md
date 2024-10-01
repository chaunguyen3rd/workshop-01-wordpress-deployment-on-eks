---
title : "Cài đặt ALB Controller"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

#### Tổng quan
**The AWS Load Balancer Controller** là bộ điều khiển Kubernetes quản lý AWS Elastic Load Balancer (ELB) cho cụm Kubernetes chạy trên Amazon EKS hoặc Kubernetes tự quản lý trên AWS. Nó tự động tạo và quản lý Application Load Balancer (ALB) và Network Load Balancer (NLB) để định tuyến lưu lượng đến các dịch vụ Kubernetes.

Trong bài lab này, chúng ta sẽ sử dụng **AWS Application Load Balancer (ALB)**.

{{% notice info %}}
Đọc thêm: https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html
{{% /notice %}}

#### Cài đặt công cụ **eksctl**.
1. Mở terminal của bạn.
    ```
      ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
    ```
  - Thay thế the ``18.206.88.146`` với địa chỉ public IP của máy EC2 của bạn.
  - Thay đổi ``~/.ssh/labBastionHostSSHKey01.pem`` thành đường dẫn của Key pair bạn đã tải về khi tạo ra máy chủ EC2.
  - Sau khi đăng nhập thành công vào EC2, chuyển sang sudo user với câu lệnh ``sudo su``.

2. Cài đặt **eksctl**.
  - Chạy đoạn code sau.
    ```
    # for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
    ARCH=amd64
    PLATFORM=$(uname -s)_$ARCH

    curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

    # (Optional) Verify checksum
    curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

    tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz

    sudo mv /tmp/eksctl /usr/local/bin
    ```
  - Kiểm tra việc cài đặt thành công với câu lệnh ``eksctl version``
    ```
    root@ip-10-0-1-234:~# eksctl version
    0.190.0
    ```

#### Cài đặt AWS Load Balancer Controller bằng Helm
1. Create IAM Role using **eksctl**.
  - Tải chính sách IAM này cho AWS Load Balancer Controller ``curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.7.2/docs/install/iam_policy.json``.
  - Tạo một chính sách IAM bằng cách sử dụng chính sách đả tải ở bước trước.
    ```
    aws iam create-policy \
      --policy-name labAWSLoadBalancerControllerPolicy \
      --policy-document file://iam_policy.json
    ```
  - Xác minh việc tạo **IAM policy** thành công.
    ```
    root@ip-10-0-1-234:~# aws iam create-policy \
      --policy-name labAWSLoadBalancerControllerPolicy \
      --policy-document file://iam_policy.json
    {
        "Policy": {
            "PolicyName": "labAWSLoadBalancerControllerPolicy",
            "PolicyId": "ANPAQIJRSMTTDGFOSBY3W",
            "Arn": "arn:aws:iam::017820706022:policy/labAWSLoadBalancerControllerPolicy",
            "Path": "/",
            "DefaultVersionId": "v1",
            "AttachmentCount": 0,
            "PermissionsBoundaryUsageCount": 0,
            "IsAttachable": true,
            "CreateDate": "2024-09-21T06:26:23+00:00",
            "UpdateDate": "2024-09-21T06:26:23+00:00"
        }
    }
    ```

2. Tạo vai trò IAM bằng cách sử dụng **eksctl**.
  - Chạy đoạn code này.
    + Change ``labEKSCluster01`` to your's cluster name.
    + Change ``017820706022`` to your account ID.
    ```
    eksctl create iamserviceaccount \
      --cluster=labEKSCluster01 \
      --namespace=kube-system \
      --name=aws-load-balancer-controller \
      --role-name labAWSLoadBalancerControllerRole \
      --attach-policy-arn=arn:aws:iam::017820706022:policy/labAWSLoadBalancerControllerPolicy \
      --approve
    ```
  - Kiểm tra việc cài đặt thành công.
    ```
    root@ip-10-0-1-234:~# kubectl -n kube-system get serviceaccount | grep aws-load-balancer-controller
    aws-load-balancer-controller                  0         81s
    ```

3. Cài đặt AWS Load Balancer Controller. 
  - Thêm **eks-charts** Helm chart repository ``helm repo add eks https://aws.github.io/eks-charts``.
  - Cập nhật repo của bạn ``helm repo update eks``.
  - Cài đặt **AWS Load Balancer Controller**.
    + Thay đổi ``labEKSCluster01`` thành tên cụm EKS của bạn.
    + Thay đổi ``vpc-091882644e7c1e207`` thành VPC ID của bạn.
    ```
    helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
      -n kube-system \
      --set clusterName=labEKSCluster01 \
      --set serviceAccount.create=false \
      --set serviceAccount.name=aws-load-balancer-controller \
      --set region=us-east-1 \
      --set vpcId=vpc-091882644e7c1e207
    ```

4. Kiểm tra việc cài đặt thành công.
    ```
    root@ip-10-0-1-234:~# helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
      -n kube-system \
      --set clusterName=labEKSCluster01 \
      --set serviceAccount.create=false \
      --set serviceAccount.name=aws-load-balancer-controller \
      --set region=us-east-1 \
      --set vpcId=vpc-091882644e7c1e207
    NAME: aws-load-balancer-controller
    LAST DEPLOYED: Sat Sep 21 06:49:02 2024
    NAMESPACE: kube-system
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    NOTES:
    AWS Load Balancer controller installed!
    root@ip-10-0-1-234:~# kubectl get deployment -n kube-system aws-load-balancer-controller
    NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
    aws-load-balancer-controller   2/2     2            2           58s
    ```

#### Thêm các tag cần thiết cho mạng con công cộng
{{% notice info %}}
Đọc thêm: https://docs.aws.amazon.com/eks/latest/userguide/alb-ingress.html
{{% /notice %}}
1. Đi đến [VPC service management console](https://console.aws.amazon.com/vpc/home)
  - Bấm **Subnets**.
  - Chọn **labPublicSubnet01**.
  - Bấm **Tags**.
  - Bấm **Manage tags**.
  ![VPC](/images/5.alb/ws01-alb01.png)

2. Ở trang **Manage tags**.
  - Bấm **Add new tag**.
  - Nhập key **kubernetes.io/role/elb** và giá trị **1**.
  - Bấm **Save**.
  
3. Làm tương tự với **labPublicSubnet02**.
  ![VPC](/images/5.alb/ws01-alb03.png)

Tiếp theo, chúng ta sẽ triển khai ứng dụng **Wordpress**