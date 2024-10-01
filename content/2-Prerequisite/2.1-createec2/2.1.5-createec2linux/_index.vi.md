---
title: "Tạo máy chủ Linux công khai"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 2.1.5 </b> "
---

### Tạo máy chủ Linux công khai

1. Đi đến [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home)

- Bấm **Instances**.
- Bấm **Launch instances**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec201.png)

2. Ở mục **Name and tags**.

- Điền vào trường **Name** với giá trị **labBastionHost01**.
- Điền vào trường **Number of instances** với giá trị **1**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec202.png)

3. Ở mục **Application and OS Images (Amazon Machine Image)**.

- Bấm vào Instance type **Ubuntu**.
- Chọn **Ubuntu Server 24.04 LTS (HVM), SSD Volume Type** ở Amazon Machine Image (AMI) trường.
- Giữ phần còn lại mặc định.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec203.png)

4. Ở mục **Instance type**.

- Chọn **t2.micro** Instance type.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec204.png)

5. Ở mục **Key pair (login)**.

- Chọn **Create new key pair**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec205.png)
- Ở popup **Create key pair**.
  - Điền vào trường **Key pair name** với giá trị **labBastionHostSSHKey01**.
  - Giữ phần còn lại mặc định.
  - Bấm **Create key pair**.
    ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec206.png)

6. Ở mục **Network settings**.

- Bấm **Edit**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec207.png)
- Ở mục **Edit**.
  {{% notice note %}}
  Bạn cần chọn mạng con labPublicSubnet01 mà chúng ta cho phép tự động gán địa chỉ IPv4 công khai trên subnet đó khi tạo VPC trước đó.
  {{% /notice %}}
  - Chọn **labVPC01** on **VPC - required**.
  - Chọn **labPublicSubnet01** on **Subnet**.
  - Chọn **Enable** on **Auto-assign public IP**.
  - Chọn **Select existing security group** on **Firewall (security groups)**.
  - Chọn **labBastionHostSG01** on **Common security groups**.
  - Bấm **Launch Instance**.
    ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec208.png)

7. Bấm **View all instances** để quay về danh sách máy chủ EC2.
   ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createec209.png)

Tiếp theo, chúng ta sẽ cấu hình máy chủ bastion Linux EC2.
