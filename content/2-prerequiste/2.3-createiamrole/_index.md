---
title : "Create IAM role"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

#### Create IAM role for Cloud9 instance

1.  We create **IAM** for the Cloud9 instance
    
    *   Select the icon **AWS Cloud9**
    *   Select **Go To Your Dashboard**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00014.png?featherlight=false&width=90pc)

2.  Then we come to the **AWS Management Console** interface
    
    *   Find and select **IAM**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00015.png?featherlight=false&width=90pc)

3.  In the **IAM** interface
    
    *   Select **Role**
    *   Select **Create role**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00016.png?featherlight=false&width=90pc)

4.  In **Select trusted entity** step
    
    *   Select **AWS service**
    *   Select **EC2**
    *   Select **Next**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00017.png?featherlight=false&width=90pc)

5.  In **Add permission** step
    
    *   Find **AdministratorAccess**
    *   Select **AdministratorAccess**
    *   Select **Next**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00018.png?featherlight=false&width=90pc)

6.  Complete **Name**
    
    *   **Name**, enter **`eks-blueprints-cdk-workshop-admin`**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00019.png?featherlight=false&width=90pc)

7.  Select **Create role**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00020.png?featherlight=false&width=90pc)

8.  Complete creation of IAM role for Cloud9 instance

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00021.png?featherlight=false&width=90pc)