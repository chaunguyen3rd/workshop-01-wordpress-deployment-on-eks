---
title : "Tạo vai trò EKS Cluster"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.2.1 </b> "
---

#### Tạo vai trò IAM **labEKSClusterRole**
1. Đi đến [IAM management console](https://console.aws.amazon.com/iam/home)
  - Bấm **Roles**.
  - Bấm **Create role**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createrole01.png)

2. Ở mục **Step 1: Select trusted entity**.
  - Ở mục **Use case**, chọn **EKS** ở trường **Service or use case**.
  - Tiếp theo, chọn **EKS - Cluster**.
  - Bấm **Next**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createrole02.png)

3. Ở mục **Step 2: Add permissions**.
  - Giữ phần còn lại mặc định và bấm **Next**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createrole03.png)

4. Ở mục **Step 3: Name, review, and create**.
  - Ở mục **Role details**, điền vào trường **Role name** với giá trị **labEKSClusterRole**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createrole04.png)
  - Kéo xuống và bấm **Create role**.
  ![VPC](/workshop-01-wordpress-deployment-on-eks/images/2.prerequisite/ws01-createrole05.png)

Tiếp theo, chúng ta sẽ tạo **labNodeGroupsRole**.