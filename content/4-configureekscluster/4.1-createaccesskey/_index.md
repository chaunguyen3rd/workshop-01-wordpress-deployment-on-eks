---
title : "Create Access key"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

In this step, we will create **Access key** for the user that configure your cluster.

#### Create **Access key**
1. Go to [IAM management console](https://console.aws.amazon.com/iam/home)
  - Click **Users**.
  - Choose **User** that you use to configure the cluster.
  ![VPC](/images/4.configure/ws01-configure02.png)

2. At **User** page.
  - Click **Security credentials** tab.
  - Click **Create access key**.
  ![VPC](/images/4.configure/ws01-configure03.png)

3. At **step 1: Access key best practices & alternatives** page.
  - Choose **Command Line Interface (CLI)**.
  - Click on **Confirmation**.
  - Click **Next**.
  ![VPC](/images/4.configure/ws01-configure04.png)

4. At **step 2: Set description tag** page.
  - Leave as default and click **Create access key**.
  ![VPC](/images/4.configure/ws01-configure05.png)

5. At **step 3: Retrieve access keys** page.
  - Save **Access key** and **Secret access key**.
  - Click **Done**
  ![VPC](/images/4.configure/ws01-configure06.png)

6. At **User** page.
  - Click **Permissions** tab.
  - Make sure this user have **AdministratorAccess** permission.
  {{% notice note %}}
  **AdministratorAccess** permission is only used in this LAB environment. If you setup for your production environment, make sure your user have at least privileges.
  {{% /notice %}}
  ![VPC](/images/4.configure/ws01-configure07.png)