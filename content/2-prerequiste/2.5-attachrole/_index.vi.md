---
title : "Gán IAM role"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 2.5 </b> "
---

#### Gán IAM role cho Cloud9 instance

1.  Đầu tiên, chúng ta đến giao diện **AWS Management Console**
    *   Tìm **ec2** và chọn **Instance**

![Create Workspace](/public/images/2-prerequiste/2.5-attachrole/001-attachrole.png?featherlight=false&width=90pc)

2.  Trong giao diện **EC2** instance

    *   Chọn **EKS Blueprint Instance**
    *   Chọn **Actions**
    *   Chọn **Security**
    *   Chọn **Modify IAM role**

![Create Workspace](/public/images/2-prerequiste/2.5-attachrole/002-attachrole.png?featherlight=false&width=90pc)

3.  Trong giao diện **Modify IAM role**
    
    *   Chọn **eks-blueprints-cdk-workshop-admin** role
    *   Chọn **Update IAM role**

![Create Workspace](/public/images/2-prerequiste/2.5-attachrole/003-attachrole.png?featherlight=false&width=90pc)