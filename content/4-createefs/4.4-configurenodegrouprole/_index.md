---
title: "Configure NodeGroup role"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4.4 </b> "
---

In this step, we will configure NodeGroup role to access the new EFS.

#### Configure **labNodeGroupsRole**

1. Go to [IAM management console](https://console.aws.amazon.com/iam/home)

- Click **Roles**.
- Choose **labNodeGroupsRole**.
  ![VPC](/workshop.chaunguyen.site/images//4.configure/ws01-configure14.png)

2. At **labNodeGroupsRole** setting page.

- Click **Add permission** and choose **Attach policies**.
  ![VPC](/workshop.chaunguyen.site/images//4.configure/ws01-configure15.png)

3. At **Add permission** page.

- Find **AmazonEFSCSIDriverPolicy** at search box.
- Choose **AmazonEFSCSIDriverPolicy** policy.
- Click **Add permissions**.
  ![VPC](/workshop.chaunguyen.site/images//4.configure/ws01-configure16.png)

Next, we will install **ALB Controller**.
