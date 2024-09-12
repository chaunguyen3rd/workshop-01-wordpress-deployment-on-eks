---
title : "Create EKS Cluster role"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.2.1 </b> "
---

#### Create IAM role **labEKSClusterRole**
1. Go to [IAM management console](https://console.aws.amazon.com/iam/home)
  - Click **Roles**.
  - Click **Create role**.
  ![VPC](/images/2.prerequisite/ws01-createrole01.png)

2. At **Step 1: Select trusted entity** section.
  - At **Use case** section, choose **EKS** at **Service or use case** field.
  - Next, choose **EKS - Cluster**.
  - Click **Next**.
  ![VPC](/images/2.prerequisite/ws01-createrole02.png)

3. At **Step 2: Add permissions** section.
  - Leave as default and click **Next**.
  ![VPC](/images/2.prerequisite/ws01-createrole03.png)

4. At **Step 3: Name, review, and create** section.
  - At **Role details** section, fill the **Role name** field with **labEKSClusterRole** value.
  ![VPC](/images/2.prerequisite/ws01-createrole04.png)
  - Scroll down and click **Create role**.
  ![VPC](/images/2.prerequisite/ws01-createrole05.png)