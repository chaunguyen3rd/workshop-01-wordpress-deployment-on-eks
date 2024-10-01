---
title : "Wordpress deployment"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : "<b> 6. </b>"
---

In this step, we will deploy the **Wordpress** application on our **EKS** cluster using **Helm**.

#### Deploy Wordpress using Helm
1. Run this code block.
    ```
    helm install my-release oci://registry-1.docker.io/bitnamicharts/wordpress --set wordpressPassword=secretpassword \
      --set persistence.storageClass=efs-sc \
      --set persistence.accessModes={ReadWriteMany} \
      --set mariadb.auth.rootPassword=secretpassword \
      --set mariadb.auth.password=secretpassword \
      --set mariadb.primary.persistence.storageClass=efs-sc \
      --set mariadb.primary.persistence.accessModes={ReadWriteMany} \
      --set service.type=NodePort \
      --set ingress.enabled=true \
      --set ingress.ingressClassName=alb \
      --set ingress.hostname=*.elb.amazonaws.com \
      --set ingress.pathType=Prefix \
      --set ingress.annotations."alb\.ingress\.kubernetes\.io\/scheme"=internet-facing \
      --set ingress.annotations."alb\.ingress\.kubernetes\.io\/target-type"=instance
    ```
2. Check if the installation success.
  {{% notice note %}}
  It will take some time for the Wordpress applications to be successfully created.
  {{% /notice %}}
  - PVC check ``kubectl get pvc``.
    ```
    root@ip-10-0-3-71:~# kubectl get pvc
    NAME                        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
    data-my-release-mariadb-0   Bound    pvc-15f668fd-24f5-4dc0-82ae-95db04b89cc5   8Gi        RWX            efs-sc         <unset>                 2m8s
    my-release-wordpress        Bound    pvc-ac35fe2b-5c94-4d62-9a0b-00a0862c4e36   10Gi       RWX            efs-sc         <unset>                 2m8s
    ```
  - All check ``kubectl get all``.
    ```
    root@ip-10-0-3-71:~# kubectl get all
    NAME                                        READY   STATUS    RESTARTS      AGE
    pod/my-release-mariadb-0                    1/1     Running   0             5m20s
    pod/my-release-wordpress-7dd64b8784-j4btb   1/1     Running   1 (97s ago)   5m20s

    NAME                           TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
    service/kubernetes             ClusterIP   172.20.0.1       <none>        443/TCP                      11d
    service/my-release-mariadb     ClusterIP   172.20.241.222   <none>        3306/TCP                     5m20s
    service/my-release-wordpress   NodePort    172.20.25.226    <none>        80:30546/TCP,443:31847/TCP   5m20s

    NAME                                   READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/my-release-wordpress   1/1     1            1           5m20s

    NAME                                              DESIRED   CURRENT   READY   AGE
    replicaset.apps/my-release-wordpress-7dd64b8784   1         1         1       5m20s

    NAME                                  READY   AGE
    statefulset.apps/my-release-mariadb   1/1     5m20s
    ```

3. Get **Wordpress** application Public URL. Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
  - On the left panel, scroll down and click **Load Balancers**.
  - Choose **k8s-default-myreleas-65aed09cf0** load balancer and click **Copy** icon on the **DNS name** **k8s-default-myreleas-65aed09cf0-694896043.us-east-1.elb.amazonaws.com**.
  ![Deploy](/workshop.chaunguyen.site/6.deploy/ws01-deploy01.png)

4. Open new browser tab.
  - User page: ``http://k8s-default-myreleas-65aed09cf0-694896043.us-east-1.elb.amazonaws.com``.
  ![Deploy](/workshop.chaunguyen.site/6.deploy/ws01-deploy02.png)
  - Admin page: ``http://k8s-default-myreleas-65aed09cf0-694896043.us-east-1.elb.amazonaws.com/admin``.
  ![Deploy](/workshop.chaunguyen.site/6.deploy/ws01-deploy03.png)

So, we have completed the deployment of Wordpress application on EKS lab.