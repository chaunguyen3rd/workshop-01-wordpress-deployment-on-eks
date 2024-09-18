---
title : "Configure the EKS cluster"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

In this step, we will configure our EKS cluster.

#### Configure EKS cluster
1. Configure **Access key** on **EC2 bastion host**.
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
    


    