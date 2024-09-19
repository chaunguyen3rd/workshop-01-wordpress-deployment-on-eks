---
title : "Configure EC2 bastion host"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 2.1.6 </b> "
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

#### Configure credential for EC2 bastion host
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
    ```
    root@ip-10-0-1-234:~# aws --version
    aws-cli/2.17.52 Python/3.12.6 Linux/6.8.0-1012-aws exe/x86_64.ubuntu.24
    ```

4. Add **Access key** on **EC2 bastion host**.
  - Run ``aws configure`` and enter your **Access key** credential.
    ```
    root@ip-10-0-1-234:~# aws configure
    AWS Access Key ID [None]: AKIAQIJRSMTTPGVD45WE
    AWS Secret Access Key [None]: ipVz+Y0C9Z2132n3Ef7jFLhJc415OXQmfq3cXPof
    Default region name [None]:
    Default output format [None]:
    root@ip-10-0-1-234:~#
    ```