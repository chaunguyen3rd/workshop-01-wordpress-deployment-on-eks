---
title : "Cấu hình máy chủ EC2"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 2.1.6 </b> "
---

Ở bước này, chúng ta sẽ tạo **Access key** cho người dùng cấu hình cụm của bạn.

#### Tạo **Access key**
1. Đi đến [IAM management console](https://console.aws.amazon.com/iam/home)
  - Bấm **Users**.
  - Chọn **User** mà bạn dùng để cấu hình cụm của bạn.
  ![VPC](/images/4.configure/ws01-configure02.png)

2. Ở trang **User**.
  - Bấm tab **Security credentials**.
  - Bấm **Create access key**.
  ![VPC](/images/4.configure/ws01-configure03.png)

3. Ở trang **step 1: Access key best practices & alternatives**.
  - Chọn **Command Line Interface (CLI)**.
  - Bấm **Confirmation**.
  - Bấm **Next**.
  ![VPC](/images/4.configure/ws01-configure04.png)

4. Ở trang **step 2: Set description tag**.
  - Giữ phần còn lại mặc định và bấm **Create access key**.
  ![VPC](/images/4.configure/ws01-configure05.png)

5. Ở trang **step 3: Retrieve access keys**.
  - Lưu **Access key** và **Secret access key**.
  - Bấm **Done**
  ![VPC](/images/4.configure/ws01-configure06.png)

6. Ở trang **User**.
  - Bấm tab **Permissions**.
  - Chắc chắn user của bạn có quyền **AdministratorAccess**.
  {{% notice note %}}
  Quyền **AdministratorAccess** chỉ có thể sử dụng ở bài lab này. Nếu bạn setup cho môi trường production, hãy chắc chắn user có ít quyền nhất có thể.
  {{% /notice %}}
  ![VPC](/images/4.configure/ws01-configure07.png)

#### Cấu hình thông tin xác thực cho máy chủ EC2 bastion
1. Đi đến [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home)
  - Copy địa chỉ IP **18.206.88.146** ở trường **Public IPv4 address**.
  ![EC2](/images/4.configure/ws01-configure01.png)  

2. Mở terminal của bạn.
    ```
      ssh ubuntu@18.206.88.146 -i ~/.ssh/labBastionHostSSHKey01.pem
    ```
  - Thay thế the ``18.206.88.146`` với địa chỉ public IP của máy EC2 của bạn.
  - Thay đổi ``~/.ssh/labBastionHostSSHKey01.pem`` thành đường dẫn của Key pair bạn đã tải về khi tạo ra máy chủ EC2.
  - Sau khi đăng nhập thành công vào EC2, chuyển sang sudo user với câu lệnh ``sudo su``.
  - Tiếp theo, cập nhật thư viện bằng ``apt update -y && apt install -y unzip``.
    
3. Tải công cụ **aws cli**.
  - Copy và chạy đoạn code sau.
    ```
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    sudo ./aws/install
    ```
  - Kiểm tra việc cài đặt thành công với câu lệnh ``aws --version``.
    ```
    root@ip-10-0-1-234:~# aws --version
    aws-cli/2.17.52 Python/3.12.6 Linux/6.8.0-1012-aws exe/x86_64.ubuntu.24
    ```

4. Thêm **Access key** vào **EC2 bastion host**.
  - Chạy ``aws configure`` và nhập **Access key**.
    ```
    root@ip-10-0-1-234:~# aws configure
    AWS Access Key ID [None]: AKIAQIJRSMTTPGVD45WE
    AWS Secret Access Key [None]: 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
    Default region name [None]:
    Default output format [None]:
    root@ip-10-0-1-234:~#
    ```

Tiếp theo, chúng ta sẽ tạo IAM cho bài lab.