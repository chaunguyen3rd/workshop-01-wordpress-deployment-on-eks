---
title: "Cleanup IAM"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: " <b> 7.6 </b> "
---

### Cleanup IAM roles and policies

#### Cleanup Access key

1. Go to [IAM management console](https://console.aws.amazon.com/iam/home)

- Click **Users**.
- Choose user that you created the **Access key** before.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup29.png)

2. At **User** page.

- Choose **Security credentials**.
- Click **Actions** and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup30.png)
- At the popup, click **Deactivate**, enter **Key** name and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup31.png)

#### Cleanup IAM roles and policies

1. Go to [IAM management console](https://console.aws.amazon.com/iam/home).

- Click **Roles**.
- Choose **Roles** as image below.
- Click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup32.png)
- At the popup, enter **delete** and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup33.png)

2. At [IAM management console](https://console.aws.amazon.com/iam/home) page.

- Click **Policies**.
- Choose **Customer managed** at **Filter by Type** option.
- Choose **labAWSLoadBalancerControllerPolicy**.
- Click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup34.png)
- At the popup, enter **labAWSLoadBalancerControllerPolicy** and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup35.png)

3. At [IAM management console](https://console.aws.amazon.com/iam/home) page.

- Click **Identity providers**.
- Choose **Your provider** that created before.
- Click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup36.png)
- At the popup, enter **confirm** and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup37.png)

So we finish cleaning up all resources needed for this lab.
