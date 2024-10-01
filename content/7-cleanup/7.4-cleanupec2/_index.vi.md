---
title : "Dọn dẹp máy chủ EC2"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 7.4 </b> "
---

### Dọn dẹp máy chủ EC2 và Security groups
1. Đi đến [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
  - Bấm **Instances**.
  - Bấm **labBastionHost01**.
  - Bấm **Instance state**.
  - Bấm **Terminate (delete) instance**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup08.png)
  - Ở popup, bấm **Terminate (Delete)**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup09.png)

2. Ở trang [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
  - Ở bảng bên trái, kéo xuống và bấm **Key Pairs**.
  - Chọn **labBastionHostSSHKey01**.
  - Bấm **Actions**.
  - Bấm **Delete**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup10.png)
  - Ở popup, nhập **Delete** và bấm **Delete**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup11.png)

3. Ở trang [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
  - Ở bảng bên trái, kéo xuống và bấm **Security Groups**.
  - Chọn **labEKSClusterSG01**, **labBastionHostSG01** và **labEFSSG01**.
  - Bấm **Actions**.
  - Bấm **Delete security groups**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup25.png)
  - Ở popup, nhập **delete** và bấm **Delete**.
  ![Cleanup](/workshop.chaunguyen.site/7.cleanup/ws01-cleanup26.png)

Tiếp theo, chúng ta sẽ dọn dẹp vpc.