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