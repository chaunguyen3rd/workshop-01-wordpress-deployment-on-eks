---
title: "Tạo EFS"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

### Tạo EFS

1. Đi đến [EFS service management console](https://console.aws.amazon.com/efs/home)

- Bấm **File systems**.
- Bấm **Create file system**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createefs01.png)

2. Ở popup **Create file system**.

- Điền vào trường **Name** với giá trị **labEFS01**.
- Điền vào **Virtual Private Cloud (VPC)** với giá trị **labVCP01**.
- Bấm **Customize**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createefs02.png)

3. Ở mục **Step 1: File system settings**.

- Giữ mọi trường mặc định.
- Bấm **Next**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createefs03.png)

4. Ở mục **Step 2: Network access**.

- Ở **us-east-1a** Availability zone, chọn **labPrivateSubnet01** subnetID and **labEFSSG01** security groups.
- Ở **us-east-1b** Availability zone, chọn **labPrivateSubnet02** subnetID and **labEFSSG01** security groups.
- Bấm **Next**.
  ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createefs04.png)

5. Giữ mặc định như **Step 3** và bấm **Next**.

6. Giữ mặc định như **Step 4** và bấm **Create**.
   ![EC2](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createefs05.png)

Tiếp theo, chúng ta sẽ cấu hình EFS CSI driver.
