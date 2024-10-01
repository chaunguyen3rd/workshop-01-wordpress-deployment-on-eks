---
title : "Create EFS"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

### Create EFS
1. Go to [EFS service management console](https://console.aws.amazon.com/efs/home)
  - Click **File systems**.
  - Click **Create file system**.
  ![EC2](/images/2.prerequisite/ws01-createefs01.png)

2. At the **Create file system** popup.
  - Fill the **Name** field with **labEFS01** value.
  - Fill the **Virtual Private Cloud (VPC)** with **labVCP01** value.
  - Click the **Customize** button.
  ![EC2](/images/2.prerequisite/ws01-createefs02.png)

3. At the **Step 1: File system settings** section.
  - Leave all fields in this step as default.
  - Click **Next** button.
  ![EC2](/images/2.prerequisite/ws01-createefs03.png)

4. At the **Step 2: Network access** section.
  - On **us-east-1a** Availability zone, choose **labPrivateSubnet01** subnetID and **labEFSSG01** security groups.
  - On **us-east-1b** Availability zone, choose **labPrivateSubnet02** subnetID and **labEFSSG01** security groups.
  - Click **Next** button.
  ![EC2](/images/2.prerequisite/ws01-createefs04.png)

5. Leave as default with **Step 3** and click **Next**.

6. Leave as default with **Step 4** and click **Create**.
  ![EC2](/images/2.prerequisite/ws01-createefs05.png)
   
Next, we will configure the EFS CSI driver.