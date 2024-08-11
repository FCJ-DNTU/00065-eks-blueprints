---
title : "Gán IAM role"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 2.4 </b> "
---

#### Gán IAM role cho Cloud9 instance

1.  Trong giao diện **Cloud9** environment
    
    *   Chọn biểu tượng Cloud9 ở gốc phải
    *   Chọn **Manage EC2 instance**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00022.png?featherlight=false&width=90pc)

2.  Trong giao diện **EC2** instance
    
    *   Chọn **Cloud9** instance
    *   Chọn **Actions**
    *   Chọn **Security**
    *   Chọn **Modify IAM role**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00023.png?featherlight=false&width=90pc)

3.  Trong giao diện **Modify IAM role**
    
    *   Chọn **eks-blueprints-cdk-workshop-admin** role
    *   Chọn **Update IAM role**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00024.png?featherlight=false&width=90pc)