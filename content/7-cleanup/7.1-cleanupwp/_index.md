---
title : "Cleanup Wordpress deployments"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 7.1 </b> "
---

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
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup01.png)

Next, we will cleanup EKS cluster.