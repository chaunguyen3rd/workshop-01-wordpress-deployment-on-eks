---
title : "Tạo vai trò NodeGroups"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2.2 </b> "
---

#### Tạo vai trò IAM **labNodeGroupsRole**
1. Đi đến [IAM management console](https://console.aws.amazon.com/iam/home)
  - Bấm **Roles**.
  - Bấm **Create role**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createrole01.png)

2. Ở mục **Step 1: Select trusted entity**.
  - Ở mục **Use case**, chọn **EC2** ở trường **Service or use case**.
  - Tiếp theo, chọn **EC2**.
  - Bấm **Next**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createrole06.png)

3. Ở mục **Step 2: Add permissions**.
  - Tìm và chọn 3 chính sách **AmazonEKS_CNI_Policy**, **AmazonEC2ContainerRegistryReadOnly** và **AmazonEKSWorkerNodePolicy**.
  - Bấm **Next**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createrole07.png)

4. Ở mục **Step 3: Name, review, and create**.
  - Ở mục **Role details**, điền vào mục **Role name** với giá trị **labNodeGroupsRole**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createrole08.png)
  - Kéo xuống và bấm **Create role**.
  ![VPC](/workshop.chaunguyen.site/2.prerequisite/ws01-createrole09.png)

Tiếp theo, chúng ta sẽ tạo cụm EKS.