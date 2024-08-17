---
title : "Attach IAM role"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 2.5 </b> "
---

#### Attach IAM Role to Cloud9 Instance

1.  **First, access the AWS Management Console**
    
    *   Search for **EC2** and select **Instance**
    
    ![Create Workspace](/public/images/2-prerequiste/2.5-attachrole/001-attachrole.png?featherlight=false&width=90pc)
    
2.  **In the EC2 instance interface**
    
    *   Select **EKS Blueprint Instance**
    *   Choose **Actions**
    *   Select **Security**
    *   Click on **Modify IAM role**
    
    ![Create Workspace](/public/images/2-prerequiste/2.5-attachrole/002-attachrole.png?featherlight=false&width=90pc)
    
3.  **In the Modify IAM role interface**
    
    *   Choose the **eks-blueprints-cdk-workshop-admin** role
    *   Click **Update IAM role**
    
    ![Create Workspace](/public/images/2-prerequiste/2.5-attachrole/003-attachrole.png?featherlight=false&width=90pc)