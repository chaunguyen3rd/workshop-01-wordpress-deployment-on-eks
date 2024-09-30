---
title : "Cleanup EFS"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 7.3 </b> "
---

### Cleanup EFS
1. Go to [EFS service management console](https://console.aws.amazon.com/efs/home)
  - Click **File systems**.
  - Choose **labEFS01**.
  ![EC2](/images/4.configure/ws01-configure13.png)

2. At **labEFS01** page.
  - Click **Delete**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup06.png)
  - At the popup, enter **fs-0003fc3d543db9be6** and click **Confirm**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup07.png)

Next, we will cleanup EC2 linux instance.