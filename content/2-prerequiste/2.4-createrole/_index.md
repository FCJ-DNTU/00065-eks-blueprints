---
title : "Create IAM Role"  
date : "`r Sys.Date()`"  
weight : 4  
chapter : false  
pre : " <b> 2.4 </b> "
---

#### Creating IAM Role for Cloud9 Instance

1.  **First, access the AWS Management Console**
    
*   Search for and select **IAM**
    
![Create Workspace](/public/images/2-prerequiste/2.4-createrole/001-createrole.png?featherlight=false&width=90pc)
    
2.  **In the IAM interface**
    
*   Select **Roles**
*   Click on **Create role**
    
![Create Workspace](/public/images/2-prerequiste/2.4-createrole/002-createrole.png?featherlight=false&width=90pc)
    
3.  **In the Select trusted entity step**
    
*   Choose **AWS service**
*   Select **EC2**
*   Click **Next**
    
![Create Workspace](/public/images/2-prerequiste/2.4-createrole/003-createrole.png?featherlight=false&width=90pc)
    
4.  **In the Add permission step**
    
*   Search for **AdministratorAccess**
*   Select **AdministratorAccess**
*   Click **Next**
    
![Create Workspace](/public/images/2-prerequiste/2.4-createrole/004-createrole.png?featherlight=false&width=90pc)
    
5.  **Complete the Name section**
*   For **Name**, enter **`eks-blueprints-cdk-workshop-admin`**
![Create Workspace](/public/images/2-prerequiste/2.4-createrole/005-createrole.png?featherlight=false&width=90pc)
    
6.  **Click Create role**
![Create Workspace](/public/images/2-prerequiste/2.4-createrole/006-createrole.png?featherlight=false&width=90pc)
    
7.  **You have successfully created an IAM role for the EC2 Instance**
![Create Workspace](/public/images/2-prerequiste/2.4-createrole/007-createrole.png?featherlight=false&width=90pc)