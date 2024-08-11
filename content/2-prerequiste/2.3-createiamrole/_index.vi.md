---
title : "Tạo IAM role"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---

#### Tạo IAM role cho Cloud9 instance

1.  Chúng ta thực hiện tạo **IAM** cho Cloud instance
    
    *   Chọn vào biểu tượng **AWS Cloud9**
    *   Chọn **Go To Your Dashboard**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00014.png?featherlight=false&width=90pc)

2.  Sau đó, chúng ta đến giao diện **AWS Management Console**
    
    *   Tìm và chọn **IAM**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00015.png?featherlight=false&width=90pc)

3.  Trong giao diện **IAM**
    
    *   Chọn **Role**
    *   Chọn **Create role**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00016.png?featherlight=false&width=90pc)

4.  Trong bước **Select trusted entity**
    
    *   Chọn **AWS service**
    *   Chọn **EC2**
    *   Chọn **Next**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00017.png?featherlight=false&width=90pc)

5.  Trong bước **Add permission**
    
    *   Tìm **AdministratorAccess**
    *   Chọn **AdministratorAccess**
    *   Chọn **Next**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00018.png?featherlight=false&width=90pc)

6.  Hoàn thành **Name**
    
    *   **Name**, nhập **`eks-blueprints-cdk-workshop-admin`**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00019.png?featherlight=false&width=90pc)

7.  Chọn **Create role**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00020.png?featherlight=false&width=90pc)

8.  Hoàn thành tạo IAM role cho Cloud9 instance

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00021.png?featherlight=false&width=90pc)