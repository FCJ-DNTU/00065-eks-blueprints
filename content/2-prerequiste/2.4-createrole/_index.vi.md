---
title : "Tạo IAM role"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 2.4 </b> "
---

#### Tạo IAM role cho Cloud9 instance

1.  Đầu tiên, chúng ta đến giao diện **AWS Management Console**
    
    *   Tìm và chọn **IAM**

![Create Workspace](/images/2-prerequiste/2.4-createrole/001-createrole.png?featherlight=false&width=90pc)


2.  Trong giao diện **IAM**
    
    *   Chọn **Role**
    *   Chọn **Create role**

![Create Workspace](/images/2-prerequiste/2.4-createrole/002-createrole.png?featherlight=false&width=90pc)

3.  Trong bước **Select trusted entity**
    
    *   Chọn **AWS service**
    *   Chọn **EC2**
    *   Chọn **Next**

![Create Workspace](/images/2-prerequiste/2.4-createrole/003-createrole.png?featherlight=false&width=90pc)

4.  Trong bước **Add permission**
    
    *   Tìm **AdministratorAccess**
    *   Chọn **AdministratorAccess**
    *   Chọn **Next**

![Create Workspace](/images/2-prerequiste/2.4-createrole/004-createrole.png?featherlight=false&width=90pc)

5.  Hoàn thành **Name**
    
    *   **Name**, nhập **`eks-blueprints-cdk-workshop-admin`**

![Create Workspace](/images/2-prerequiste/2.4-createrole/005-createrole.png?featherlight=false&width=90pc)

6.  Chọn **Create role**

![Create Workspace](/images/2-prerequiste/2.4-createrole/006-createrole.png?featherlight=false&width=90pc)

7.  Hoàn thành tạo IAM role cho EC2 Instance
![Create Workspace](/images/2-prerequiste/2.4-createrole/007-createrole.png?featherlight=false&width=90pc)