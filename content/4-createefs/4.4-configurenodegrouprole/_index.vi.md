---
title: "Cấu hình vai trò NodeGroup"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4.4 </b> "
---

Ở bước này, chúng ta sẽ cấu hình vai trò NodeGroup để truy cập đến EFS.

#### Cấu hình **labNodeGroupsRole**

1. Đi đến [IAM management console](https://console.aws.amazon.com/iam/home)

- Bấm **Roles**.
- Chọn **labNodeGroupsRole**.
  ![VPC](/workshop.chaunguyen.site/images//4.configure/ws01-configure14.png)

2. Ở trang thiết lập **labNodeGroupsRole**.

- Bấm **Add permission** and chọn **Attach policies**.
  ![VPC](/workshop.chaunguyen.site/images//4.configure/ws01-configure15.png)

3. Ở trang **Add permission**.

- Tìm **AmazonEFSCSIDriverPolicy** ở ô tìm kiếm.
- Chọn chính sách **AmazonEFSCSIDriverPolicy**.
- Bấm **Add permissions**.
  ![VPC](/workshop.chaunguyen.site/images//4.configure/ws01-configure16.png)

Tiếp theo, chúng ta sẽ cài đặt **ALB Controller**.
