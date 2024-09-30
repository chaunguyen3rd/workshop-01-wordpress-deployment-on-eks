---
title : "Tạo IAM Role"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

### Tổng quan

**IAM roles in AWS (Identity and Access Management)** là một cách để cấp quyền cụ thể cho người dùng, dịch vụ hoặc ứng dụng mà không cần sử dụng danh tính riêng của họ. Thay vì bị ràng buộc với một người dùng duy nhất, các vai trò IAM có thể được các thực thể đáng tin cậy đảm nhận tạm thời, cho phép họ thực hiện các hành động dựa trên các quyền được liên kết với vai trò đó.

Vai trò IAM thường được sử dụng cho:

- **Truy cập liên tài khoản**: Cho phép người dùng hoặc dịch vụ trong một tài khoản AWS truy cập tài nguyên trong một tài khoản khác.
- **Quyền dịch vụ**: Cấp cho các dịch vụ AWS (như EC2 hoặc Lambda) các quyền cần thiết để tương tác với các dịch vụ AWS khác.
- **Người dùng ngoài AWS**: Cấp quyền cho những người dùng đã được xác thực bên ngoài AWS (ví dụ: thông qua nhà cung cấp danh tính bên ngoài).
  
Vai trò IAM được xác định bởi chính sách chỉ rõ hành động nào được phép hoặc bị từ chối và được đảm nhận bằng cách gọi API `sts:AssumeRole`, cung cấp thông tin xác thực bảo mật tạm thời trong suốt phiên.

### Tạo IAM Role

Ở bước này, chúng ta sẽ tiến hành tạo các vai trò và chính sách IAM cần thiết để hoàn thành bài thực hành này.

### Nội dung
  - [Create labEKSClusterRole](2.2.1-createeksclusterrole/)
  - [Create labNodeGroupsRole](2.2.2-createnodegrouprole/)
