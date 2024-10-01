---
title: "Cleanup EC2 linux instance"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 7.4 </b> "
---

### Cleanup EC2 linux bastion host and Security groups

1. Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).

- Click **Instances**.
- Choose **labBastionHost01**.
- Click **Instance state**.
- Click **Terminate (delete) instance**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup08.png)
- At the popup, click **Terminate (Delete)**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup09.png)

2. At [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home) page.

- On the left panel, scroll down and click **Key Pairs**.
- Choose **labBastionHostSSHKey01**.
- Click **Actions**.
- Click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup10.png)
- At the popup, enter **Delete** and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup11.png)

3. At [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home) page.

- On the left panel, scroll down and click **Security Groups**.
- Choose **labEKSClusterSG01**, **labBastionHostSG01** and **labEFSSG01**.
- Click **Actions**.
- Click **Delete security groups**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup25.png)
- At the popup, enter **delete** and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup26.png)

Next, we will cleanup vpc.
