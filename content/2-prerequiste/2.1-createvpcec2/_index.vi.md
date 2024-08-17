---
title : "Tạo VPC và EC2 Instance"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

#### Tạo VPC

1.  Truy cập [AWS Management Console](https://aws.amazon.com/vi/console/)
    
    *   Tìm **VPC**
    *   Chọn **Create VPC**
    

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/001-createvpcec2.png?featherlight=false&width=90pc)

2.  Trong giao diện **VPC settings**
    
    *   **Resources to create**, chọn **VPC and more**
    *   **Name tag auto-generation**, nhập **EKS Blueprint VPC**
    *   **IPv4 CIDR block**, nhập **10.0.0.0/16**

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/002-createvpcec2.png?featherlight=false&width=30pc)

3.  Chọn các **AZs** 
    *   Chọn các AZs theo hình và bấm chọn **Create VPC** 

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/003-createvpcec2.png?featherlight=false&height=30pc)

4.  Sau khi tạo xong, chúng ta sẽ có một VPC như thế này
![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/004-createvpcec2.png?featherlight=false&width=90pc)
![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/005-createvpcec2.png?featherlight=false&width=90pc)

#### Tạo EC2 Instance 

1.  Truy cập [AWS Management Console](https://aws.amazon.com/vi/console/)
    
    *   Tìm **EC2**
    *   Chọn **Launch Instance**
    

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/000-createvpcec2.png?featherlight=false&width=90pc)

2.  Trong giao diện **Launch an instance**
    
    *   **Name and tags**, chọn **EKS Blueprint Instance**

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/006-createvpcec2.png?featherlight=false&width=90pc)

3.  Ở mục **Application and OS Images (Amazon Machine Image)**

    *   Chọn **Amazon Linux 2023 AMI**

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/007-createvpcec2.png?featherlight=false&height=30pc)

4.  Ở mục **Instance type** và **Key pair**

    *   Chọn **t3.small**
    *   Tạo ra 1 **key pair** đặt tên là **kp-eks-blueprint**
![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/008-createvpcec2.png?featherlight=false&height=30pc)

5.  Ở mục **Network settings**

    *   Chọn VPC mà bạn mới tạo
    *   Chọn **public-subnet-1**
    *   Bật **Auto-assign public IP** 
    *   Tạo một **Security Group**

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/009-createvpcec2.png?featherlight=false&height=50pc)


6.  Ở mục **Configure storage** thay đổi bộ nhớ thành **30GB** va nhấn **Launch Instance** 

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/010-createvpcec2.png?featherlight=false&width=90pc)



7.  Vậy là chúng ta đã hoàn thành việc khởi tạo EC2 Instance.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/011-createvpcec2.png?featherlight=false&width=90pc)

