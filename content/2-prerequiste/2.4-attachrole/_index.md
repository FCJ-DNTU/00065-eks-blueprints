---
title : "Assign IAM role"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---

#### Assign IAM role to Cloud9 instance

1.  In the **Cloud9** environment interface
    
    *   Select the Cloud9 icon on the right root
    *   Select **Manage EC2 instance**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00022.png?featherlight=false&width=90pc)

2.  In the **EC2** instance . interface
    
    *   Select **Cloud9** instance
    *   Select **Actions**
    *   Select **Security**
    *   Select **Modify IAM role**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00023.png?featherlight=false&width=90pc)

3.  In the **Modify IAM role** interface
    
    *   Select **eks-blueprints-cdk-workshop-admin** role
    *   Select **Update IAM role**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00024.png?featherlight=false&width=90pc)