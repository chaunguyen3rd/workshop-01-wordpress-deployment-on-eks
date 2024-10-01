---
title: "Dọn dẹp Wordpress deployments"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 7.1 </b> "
---

### Dọn dẹp Wordpress deployments

1. Mở terminal của bạn.
   ```
     ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
   ```

- Thay thế the `18.206.88.146` với địa chỉ public IP của máy EC2 của bạn.
- Thay đổi `~/.ssh/labBastionHostSSHKey01.pem` thành đường dẫn của Key pair bạn đã tải về khi tạo ra máy chủ EC2.
- Sau khi đăng nhập thành công vào EC2, chuyển sang sudo user với câu lệnh `sudo su`.
- Chạy `helm uninstall my-release` để dọn dẹp deployments **Wordpress**.
  ```
  root@ip-10-0-3-71:~# helm uninstall my-release
  release "my-release" uninstalled
  root@ip-10-0-3-71:~# kubectl get all
  NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
  service/kubernetes   ClusterIP   172.20.0.1   <none>        443/TCP   11d
  ```
- Tiếp theo, chạy `kubectl delete pvc data-my-release-mariadb-0` để dọn dẹp **pvc**.
  ```
  root@ip-10-0-3-71:~# kubectl get pvc
  NAME                        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
  data-my-release-mariadb-0   Bound    pvc-658e3095-b40b-4539-83d6-adebfdfe1c67   8Gi        RWX            efs-sc         <unset>                 3h18m
  root@ip-10-0-3-71:~# kubectl delete pvc data-my-release-mariadb-0
  persistentvolumeclaim "data-my-release-mariadb-0" deleted
  ```

2. Đi đến [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).

- Ở bảng bên trái, kéo xuống và bấm **Load Balancers**.
- Đến đây, chúng ta sẽ không thấy cân bằng tải **k8s-default-myreleas-65aed09cf0** nữa.
  ![Cleanup](/workshop-01-wordpress-deployment-on-eks/images/7.cleanup/ws01-cleanup01.png)

Tiếp theo, chúng ta sẽ dọn dẹp cụm EKS.
