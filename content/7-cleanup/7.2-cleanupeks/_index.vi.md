---
title : "Dọn dẹp cụm EKS"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 7.2 </b> "
---

### Dọn dẹp Node group
1. Đi đến [EKS management console](https://console.aws.amazon.com/eks/home).
  - Bấm **Clusters**.
  - Chọn **labEKSCluster01**.
  ![Connect](/workshop.chaunguyen.site/4.configure/ws01-configure12.png)

2. Ở trang **labEKSCluster01**.
  - Bấm **Compute**.
  - Chọn **labNodeGroup01**.
  - Bấm **Delete**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup02.png)
  - Ở popup, nhập **labNodeGroup01** và bấm **Delete**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup03.png)
  {{% notice note %}}
  Sẽ mất một thời gian để xóa thành công nhóm Node.
  {{% /notice %}}

### Dọn dẹp cụm EKS
1. Đi đến [EKS management console](https://console.aws.amazon.com/eks/home).
  - Bấm **Clusters**.
  - Chọn **labEKSCluster01**.
  ![Connect](/workshop.chaunguyen.site/4.configure/ws01-configure12.png)

2. Ở trang **labEKSCluster01**.
  - Bấm **Delete cluster**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup04.png)
  - Ở popup, nhập **labEKSCluster01** và bấm **Delete**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup05.png)
  {{% notice note %}}
  Sẽ mất một thời gian để xóa thành công cụm EKS.
  {{% /notice %}}

Next, we will cleanup EFS.