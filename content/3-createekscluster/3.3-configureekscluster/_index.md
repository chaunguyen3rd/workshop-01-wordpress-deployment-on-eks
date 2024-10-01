---
title: "Configure the EKS cluster"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

In this step, we will configure our EKS cluster.

#### Create **Access entry** to connect to EKS cluster

1. Go to [EKS management console](https://console.aws.amazon.com/eks/home).

- Click on **Clusters**.
- Choose **labEKSCluster01**.
  ![Connect](/workshop.chaunguyen.site/images//4.configure/ws01-configure12.png)

2. At **labEKSCluster01** page.

- Click **Access** tab.
- Click **Create access entry**.
  ![Connect](/workshop.chaunguyen.site/images//4.configure/ws01-configure08.png)

3. At **step 1: Configure IAM access entry**.

- Change `arn:aws:iam::017820706022:user/chaunguyen-admin` to your IAM user used to connect to the EKS cluster.
  ![Connect](/workshop.chaunguyen.site/images//4.configure/ws01-configure09.png)
- Scroll down and click **Next**.

4. At **step 2: Add access policy**.

- Choose **AmazonEKSClusterAdminPolicy** at **Policy name** field.
- Click **Add policy**.
- Click **Next**.
  ![Connect](/workshop.chaunguyen.site/images//4.configure/ws01-configure10.png)

5. At **step 3: Review and create**.

- Leave as default and click **Create**.
  ![Connect](/workshop.chaunguyen.site/images//4.configure/ws01-configure11.png)

#### Configure the EKS cluster

1. Open your terminal.
   ```
     ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
   ```

- Change the `18.206.88.146` to your EC2's Public IP address.
- Change the `~/.ssh/labBastionHostSSHKey01.pem` to the path of the Key pair you downloaded when creating your EC2 instance.
- After successful login to your EC2, switch to sudo user with `sudo su`.

2. Connect to your EKS cluster.

- `aws eks update-kubeconfig --region <region-code> --name <my-cluster>
`. + Change <region-code> to your **Region code**. + Change <my-cluster> to your **EKS cluster name**.
  `    root@ip-10-0-1-234:~# aws eks update-kubeconfig --region us-east-1 --name labEKSCluster01
    Added new context arn:aws:eks:us-east-1:017820706022:cluster/labEKSCluster01 to /root/.kube/config
   `
- Check if the connection success.
  ```
  root@ip-10-0-1-234:~# kubectl get nodes
  NAME                          STATUS   ROLES    AGE   VERSION
  ip-10-0-11-248.ec2.internal   Ready    <none>   44h   v1.30.2-eks-1552ad0
  ip-10-0-12-93.ec2.internal    Ready    <none>   44h   v1.30.2-eks-1552ad0
  ```
