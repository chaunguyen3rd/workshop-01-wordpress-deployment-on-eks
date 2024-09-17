---
title : "Connect to EKS cluster"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

In this step, we will use the **Bastion host (EC2 linux in public subnet)** created before to connect and install some stuffs for our EKS cluster.

#### Connect to EC2 linux
1. Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home)
  - Copy the IP **18.206.88.146** at **Public IPv4 address** field.
  ![EC2](/images/4.configure/ws01-configure01.png)  

2. Open your terminal.
    ```
      ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
    ```
  - Change the ``18.206.88.146`` to your EC2's Public IP address.
  - Change the ``~/.ssh/labBastionHostSSHKey01.pem`` to the path of the Key pair you downloaded when creating your EC2 instance.
  - After successful login to your EC2, switch to sudo user with ``sudo su``.
  - Next, update the libraries with ``apt update -y && apt install -y unzip``.
    
3. Install **aws cli** tool.
  - Copy and run this code block.
    ```
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    sudo ./aws/install
    ```
  - Confirm the installation with ``aws --version``.
 
4. Install **kubectl** tool.

Next, we will proceed to create an S3 bucket to store session logs.