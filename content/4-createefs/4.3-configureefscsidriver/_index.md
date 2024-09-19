---
title : "Configure EFS CSI driver"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

In this step, we will configure our EFS CSI driver.

#### Create **Access entry** to connect to EKS cluster
1. Go to [EKS management console](https://console.aws.amazon.com/eks/home).
  - Click on **Clusters**.
  - Choose **labEKSCluster01**.
  ![Connect](/images/4.configure/ws01-configure12.png)

2. At **labEKSCluster01** page.
  - Click **Access** tab.
  - Click **Create access entry**.
  ![Connect](/images/4.configure/ws01-configure08.png)

3. At **step 1: Configure IAM access entry**.
  - Change ``arn:aws:iam::017820706022:user/chaunguyen-admin`` to your IAM user used to connect to the EKS cluster.
  ![Connect](/images/4.configure/ws01-configure09.png)
  - Scroll down and click **Next**.

4. At **step 2: Add access policy**.
  - Choose **AmazonEKSClusterAdminPolicy** at **Policy name** field.
  - Click **Add policy**.
  - Click **Next**.
  ![Connect](/images/4.configure/ws01-configure10.png)

5. At **step 3: Review and create**.
  - Leave as default and click **Create**.
  ![Connect](/images/4.configure/ws01-configure11.png)

#### Configure the EKS cluster
1. Add **Access key** on **EC2 bastion host**.
  - At your last SSH session.
  - Run ``aws configure`` and enter your **Access key** credential.
    ```
    root@ip-10-0-1-234:~# aws configure
    AWS Access Key ID [None]: AKIAQIJRSMTTPGVD45WE
    AWS Secret Access Key [None]: ipVz+Y0C9Z2132n3Ef7jFLhJc415OXQmfq3cXPof
    Default region name [None]:
    Default output format [None]:
    root@ip-10-0-1-234:~#
    ```

2. Connect to your EKS cluster.
  - ``aws eks update-kubeconfig --region <region-code> --name <my-cluster>
``.
    + Change <region-code> to your **Region code**.
    + Change <my-cluster> to your **EKS cluster name**.
    ```
    root@ip-10-0-1-234:~# aws eks update-kubeconfig --region us-east-1 --name labEKSCluster01
    Added new context arn:aws:eks:us-east-1:017820706022:cluster/labEKSCluster01 to /root/.kube/config
    ```
  - Check if the connection success.
    ```
    root@ip-10-0-1-234:~# kubectl get nodes
    NAME                          STATUS   ROLES    AGE   VERSION
    ip-10-0-11-248.ec2.internal   Ready    <none>   44h   v1.30.2-eks-1552ad0
    ip-10-0-12-93.ec2.internal    Ready    <none>   44h   v1.30.2-eks-1552ad0
    ```    


    