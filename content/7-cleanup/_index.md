---
title : "Cleanup"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---

### Overall
In this step, we will clean up the resources created in the lab to avoid incurring costs.

### Cleanup Wordpress deployments
1. Open your terminal.
    ```
      ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
    ```
  - Change the ``18.206.88.146`` to your EC2's Public IP address.
  - Change the ``~/.ssh/labBastionHostSSHKey01.pem`` to the path of the Key pair you downloaded when creating your EC2 instance.
  - After successful login to your EC2, switch to sudo user with ``sudo su``.
  - Run ``helm uninstall my-release`` to cleanup **Wordpress** deployments.
    ```
    root@ip-10-0-3-71:~# helm uninstall my-release
    release "my-release" uninstalled
    root@ip-10-0-3-71:~# kubectl get all
    NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
    service/kubernetes   ClusterIP   172.20.0.1   <none>        443/TCP   11d
    ```
  - Next, run ``kubectl delete pvc data-my-release-mariadb-0`` to cleanup **pvc**.
    ```
    root@ip-10-0-3-71:~# kubectl get pvc
    NAME                        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
    data-my-release-mariadb-0   Bound    pvc-658e3095-b40b-4539-83d6-adebfdfe1c67   8Gi        RWX            efs-sc         <unset>                 3h18m
    root@ip-10-0-3-71:~# kubectl delete pvc data-my-release-mariadb-0
    persistentvolumeclaim "data-my-release-mariadb-0" deleted
    ```

2. Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
  - On the left panel, scroll down and click **Load Balancers**.
  - This time, we won't see **k8s-default-myreleas-65aed09cf0** load balancer anymore.
  ![Cleanup](/images/7.cleanup/ws01-cleanup01.png)

### Cleanup Node group
1. Go to [EKS management console](https://console.aws.amazon.com/eks/home).
  - Click on **Clusters**.
  - Choose **labEKSCluster01**.
  ![Connect](/images/4.configure/ws01-configure12.png)

2. At **labEKSCluster01** page.
  - Click **Compute**.
  - Choose **labNodeGroup01**.
  - Click **Delete**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup02.png)
  - At the popup, enter **labNodeGroup01** and click **Delete**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup03.png)
  {{% notice note %}}
  It will take some time for the Node group to be successfully deleted.
  {{% /notice %}}

### Cleanup EKS cluster
1. Go to [EKS management console](https://console.aws.amazon.com/eks/home).
  - Click on **Clusters**.
  - Choose **labEKSCluster01**.
  ![Connect](/images/4.configure/ws01-configure12.png)

2. At **labEKSCluster01** page.
  - Click **Delete cluster**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup04.png)
  - At the popup, enter **labEKSCluster01** and click **Delete**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup05.png)
  {{% notice note %}}
  It will take some time for the Node group to be successfully deleted.
  {{% /notice %}}

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

### Cleanup EC2 linux bastion host
1. Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
  - Click **Instances**.
  - Choose **labBastionHost01**.
  - Click **Instance state**.
  - Click **Terminate (delete) instance**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup08.png)
  - At the popup, click **Terminate (Delete)**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup09.png)

2. At [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
  - On the left panel, scroll down and click **Key Pairs**.
  - Choose **labBastionHostSSHKey01**.
  - Click **Actions**.
  - Click **Delete**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup10.png)
  - At the popup, enter **Delete** and click **Delete**.
  ![Cleanup](/images/7.cleanup/ws01-cleanup11.png)

### Cleanup EC2 linux bastion host
