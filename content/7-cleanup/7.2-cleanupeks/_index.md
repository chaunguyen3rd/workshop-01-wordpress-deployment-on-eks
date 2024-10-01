---
title : "Cleanup EKS cluster"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 7.2 </b> "
---

### Cleanup Node group
1. Go to [EKS management console](https://console.aws.amazon.com/eks/home).
  - Click on **Clusters**.
  - Choose **labEKSCluster01**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/4.configure/ws01-configure12.png)

2. At **labEKSCluster01** page.
  - Click **Compute**.
  - Choose **labNodeGroup01**.
  - Click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup02.png)
  - At the popup, enter **labNodeGroup01** and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup03.png)
  {{% notice note %}}
  It will take some time for the Node group to be successfully deleted.
  {{% /notice %}}

### Cleanup EKS cluster
1. Go to [EKS management console](https://console.aws.amazon.com/eks/home).
  - Click on **Clusters**.
  - Choose **labEKSCluster01**.
  ![Connect](/workshop-01-wordpress-deployment-on-eks/images/4.configure/ws01-configure12.png)

2. At **labEKSCluster01** page.
  - Click **Delete cluster**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup04.png)
  - At the popup, enter **labEKSCluster01** and click **Delete**.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup05.png)
  {{% notice note %}}
  It will take some time for the EKS cluster to be successfully deleted.
  {{% /notice %}}

Next, we will cleanup EFS.