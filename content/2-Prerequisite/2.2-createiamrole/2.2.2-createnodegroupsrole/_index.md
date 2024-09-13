---
title : "Create NodeGroups role"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2.2 </b> "
---

#### Create IAM role **labNodeGroupsRole**
1. Go to [IAM management console](https://console.aws.amazon.com/iam/home)
  - Click **Roles**.
  - Click **Create role**.
  ![VPC](/images/2.prerequisite/ws01-createrole01.png)

2. At **Step 1: Select trusted entity** section.
  - At **Use case** section, choose **EC2** at **Service or use case** field.
  - Next, choose **EC2**.
  - Click **Next**.
  ![VPC](/images/2.prerequisite/ws01-createrole06.png)

3. At **Step 2: Add permissions** section.
  - Find and choose three policies **AmazonEKS_CNI_Policy**, **AmazonEC2ContainerRegistryReadOnly** and **AmazonEKSWorkerNodePolicy**.
  - Click **Next**.
  ![VPC](/images/2.prerequisite/ws01-createrole07.png)

4. At **Step 3: Name, review, and create** section.
  - At **Role details** section, fill the **Role name** field with **labNodeGroupsRole** value.
  ![VPC](/images/2.prerequisite/ws01-createrole08.png)
  - Scroll down and click **Create role**.
  ![VPC](/images/2.prerequisite/ws01-createrole09.png)