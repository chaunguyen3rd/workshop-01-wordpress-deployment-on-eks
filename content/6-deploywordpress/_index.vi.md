---
title: "Triển khai Wordpress"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<b> 6. </b>"
---

Ở bước này, chúng ta sẽ triển khai ứng dụng **Wordpress** trên cụm **EKS** của chúng ta bằng cách sử dụng **Helm**.

#### Triển khai Wordpress bằng cách dùng Helm

1. Chạy đoạn code này.
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
2. Kiểm tra việc cài đặt thành công.
   {{% notice note %}}
   Sẽ mất một thời gian để tạo thành công ứng dụng Wordpress.
   {{% /notice %}}

- Kiểm tra PVC `kubectl get pvc`.
  ```
  root@ip-10-0-3-71:~# kubectl get pvc
  NAME                        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
  data-my-release-mariadb-0   Bound    pvc-15f668fd-24f5-4dc0-82ae-95db04b89cc5   8Gi        RWX            efs-sc         <unset>                 2m8s
  my-release-wordpress        Bound    pvc-ac35fe2b-5c94-4d62-9a0b-00a0862c4e36   10Gi       RWX            efs-sc         <unset>                 2m8s
  ```
- Kiểm tra các thành phần khác `kubectl get all`.

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

3. Lấy URL công cộng của ứng dụng **Wordpress**. Đi đến [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).

- Ở bảng bên trái, kéo xuống và bấm **Load Balancers**.
- Chọn **k8s-default-myreleas-65aed09cf0** load balancer và bấm biểu tượng **Copy** ở **DNS name** **k8s-default-myreleas-65aed09cf0-694896043.us-east-1.elb.amazonaws.com**.
  ![Deploy](/workshop.chaunguyen.site/images//6.deploy/ws01-deploy01.png)

4. Mở một tab trình duyệt mới.

- Trang người dùng: `http://k8s-default-myreleas-65aed09cf0-694896043.us-east-1.elb.amazonaws.com`.
  ![Deploy](/workshop.chaunguyen.site/images//6.deploy/ws01-deploy02.png)
- Trang quản trị: `http://k8s-default-myreleas-65aed09cf0-694896043.us-east-1.elb.amazonaws.com/admin`.
  ![Deploy](/workshop.chaunguyen.site/images//6.deploy/ws01-deploy03.png)

Vậy là chúng ta đã hoàn thành bài lab về việc triển khai ứng dụng Wordpress trên cụm EKS.
