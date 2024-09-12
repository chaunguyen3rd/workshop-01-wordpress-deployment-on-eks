---
title : "Create Public instance"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.1.5 </b> "
---

1. Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home)
  - Click **Instances**.
  - Click **Launch instances**.
  ![EC2](/images/2.prerequisite/ws01-createec201.png)  

2. At the **Name and tags** section.
  - Fill the **Name** field with **labBastionHost01** value.
  - Fill the **Number of instances** with **1** value.
  ![EC2](/images/2.prerequisite/ws01-createec202.png)

3. At the **Application and OS Images (Amazon Machine Image)** section.
  - Click on Instance type **Ubuntu**.
  - Choose **Ubuntu Server 24.04 LTS (HVM), SSD Volume Type** on Amazon Machine Image (AMI) field.
  - Leave the rest as default.
  ![EC2](/images/2.prerequisite/ws01-createec203.png)

4. At the **Instance type** section.
  - Choose **t2.micro** Instance type.
  ![EC2](/images/2.prerequisite/ws01-createec204.png)

5. At the **Key pair (login)** section.
  - Click on the **Create new key pair**.
  ![EC2](/images/2.prerequisite/ws01-createec205.png)
  - At the **Create key pair** popup.
    + Fill the **Key pair name** field with **labBastionHostSSHKey01** value.
    + Leave the rest as default.
    + Click **Create key pair** button.
    ![EC2](/images/2.prerequisite/ws01-createec206.png)

6. At the **Network settings** section.
  - Click the **Edit** button.
  ![EC2](/images/2.prerequisite/ws01-createec207.png)
  - At the **Edit** sections.
  {{% notice note %}}
  You need to choose labPublicSubnet01 subnet which we allow Enable auto-assign public IPv4 address on that subnet when creating VPC before.
  {{% /notice %}}
    + Choose **labVPC01** on **VPC - required** field.
    + Choose **labPublicSubnet01** on **Subnet** field.
    + Choose **Enable** on **Auto-assign public IP** field.
    + Choose **Select existing security group** on **Firewall (security groups)** field.
    + Choose **labBastionHostSG01** on **Common security groups** field.
    + Click **Launch Instance** button.
    ![EC2](/images/2.prerequisite/ws01-createec208.png)

7. Click **View all instances** to return to the list of EC2 instances.
  ![EC2](/images/2.prerequisite/ws01-createec209.png)

Next, we will create EFS for EKS cluster connect to later.