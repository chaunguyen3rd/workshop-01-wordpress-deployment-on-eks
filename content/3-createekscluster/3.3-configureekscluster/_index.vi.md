---
title: "Cấu hình cụm EKS"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

Ở bước này, chúng ta sẽ cấu hình cụm EKS.

#### Tạo **Access entry** để kết nối tới cụm EKS

1. Đi đến [EKS management console](https://console.aws.amazon.com/eks/home).

- Bấm **Clusters**.
- Chọn **labEKSCluster01**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/4.configure/ws01-configure12.png)

2. Ở trang **labEKSCluster01**.

- Bấm tab **Access**.
- Bấm **Create access entry**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/4.configure/ws01-configure08.png)

3. Ở **step 1: Configure IAM access entry**.

- Thay đổi `arn:aws:iam::017820706022:user/chaunguyen-admin` thành giá trị IAM user của bạn.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/4.configure/ws01-configure09.png)
- Kéo xuống và bấm **Next**.

4. Ở **step 2: Add access policy**.

- Chọn trường **AmazonEKSClusterAdminPolicy** ở **Policy name**.
- Chọn **Add policy**.
- Chọn **Next**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/4.configure/ws01-configure10.png)

5. Ở **step 3: Review and create**.

- Giữ mặc định và bấm **Create**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/4.configure/ws01-configure11.png)

#### Cấu hình cụm EKS

1. Mở terminal của bạn.
   ```
     ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
   ```

- Thay thế the `18.206.88.146` với địa chỉ public IP của máy EC2 của bạn.
- Thay đổi `~/.ssh/labBastionHostSSHKey01.pem` thành đường dẫn của Key pair bạn đã tải về khi tạo ra máy chủ EC2.
- Sau khi đăng nhập thành công vào EC2, chuyển sang sudo user với câu lệnh `sudo su`.

2. Kết nối tới cụm EKS.

- `aws eks update-kubeconfig --region <region-code> --name <my-cluster>
`. + Change <region-code> to your **Region code**. + Change <my-cluster> to your **EKS cluster name**.
  `    root@ip-10-0-1-234:~# aws eks update-kubeconfig --region us-east-1 --name labEKSCluster01
    Added new context arn:aws:eks:us-east-1:017820706022:cluster/labEKSCluster01 to /root/.kube/config
   `
- Kiểm tra nếu kết nối thành công hay không.
  ```
  root@ip-10-0-1-234:~# kubectl get nodes
  NAME                          STATUS   ROLES    AGE   VERSION
  ip-10-0-11-248.ec2.internal   Ready    <none>   44h   v1.30.2-eks-1552ad0
  ip-10-0-12-93.ec2.internal    Ready    <none>   44h   v1.30.2-eks-1552ad0
  ```
