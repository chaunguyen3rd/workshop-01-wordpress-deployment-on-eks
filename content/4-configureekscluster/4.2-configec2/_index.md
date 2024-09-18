---
title : "Configure the public EC2"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

In this step, we will use the **Bastion host (EC2 linux in public subnet)** created before to install some stuffs for our EKS cluster.

#### Configure the EC2 bastion host
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
4. Install **kubectl** tool.
  - Copy and run this code block.
    ```
    curl -O https://s3.cn-north-1.amazonaws.com.cn/amazon-eks/1.30.2/2024-07-12/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH
    echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
    ```
  - Confirm the installation with ``kubectl version --client``.
    ```
    root@ip-10-0-1-234:~# kubectl version --client
    Client Version: v1.30.2-eks-1552ad0
    ```

5. Install **helm** tool.
  {{% notice info %}}
  Helm is a package manager for Kubernetes that simplifies the process of deploying and managing applications within a Kubernetes cluster. Read more: https://helm.sh/docs/
  {{% /notice %}}
  - Copy and run this code block.
    ```
    curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
    sudo apt-get install apt-transport-https --yes
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
    sudo apt-get update
    sudo apt-get install helm
    ```
  - Confirm the installation with ``helm version``.
    ```
    root@ip-10-0-1-234:~# helm version
    version.BuildInfo{Version:"v3.16.1", GitCommit:"5a5449dc42be07001fd5771d56429132984ab3ab", GitTreeState:"clean", GoVersion:"go1.22.7"}
    ```

Next, we will proceed to configure the **EKS cluster**.