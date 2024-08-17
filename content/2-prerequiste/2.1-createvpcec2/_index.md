---
title : "Create VPC và EC2 Instance"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

### Create a VPC

1.  **Access AWS Management Console:**
    *   Search for **VPC**.
    *   Select **Create VPC**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/001-createvpcec2.png?featherlight=false&width=90pc)

2.  **VPC Settings:**
    *   In the **Resources to create** section, select **VPC and more**.
    *   In **Name tag auto-generation**, enter **EKS Blueprint VPC**.
    *   In **IPv4 CIDR block**, enter **10.0.0.0/16**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/002-createvpcec2.png?featherlight=false&width=30pc)

3.  **Select Availability Zones (AZs):**
    *   Choose the AZs as shown in the image and click **Create VPC**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/003-createvpcec2.png?featherlight=false&height=30pc)

4.  **Completion:**
    *   After creation, you will have a VPC that looks like this.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/004-createvpcec2.png?featherlight=false&width=90pc) ![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/005-createvpcec2.png?featherlight=false&width=90pc)

### Create an EC2 Instance

1.  **Access AWS Management Console:**
    *   Search for **EC2**.
    *   Select **Launch Instance**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/000-createvpcec2.png?featherlight=false&width=90pc)

2.  **Launch an Instance:**
    *   In the **Name and tags** section, enter **EKS Blueprint Instance**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/006-createvpcec2.png?featherlight=false&width=90pc)

3.  **Select AMI:**
    *   In the **Application and OS Images (Amazon Machine Image)** section, choose **Amazon Linux 2023 AMI**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/007-createvpcec2.png?featherlight=false&height=30pc)

4.  **Instance Type and Key Pair:**
    *   Choose **t3.small**.
    *   Create a **key pair** and name it **kp-eks-blueprint**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/008-createvpcec2.png?featherlight=false&height=30pc)

5.  **Network Settings:**
    *   Select the VPC you just created.
    *   Choose **public-subnet-1**.
    *   Enable **Auto-assign public IP**.
    *   Create a **Security Group**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/009-createvpcec2.png?featherlight=false&height=50pc)

6.  **Configure Storage:**
    *   Change the storage size to **30GB** and click **Launch Instance**.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/010-createvpcec2.png?featherlight=false&width=90pc)

7.  **Completion:**
    *   You have successfully created an EC2 Instance.

![Create Workspace](/public/images/2-prerequiste/2.1-createvpcec2/011-createvpcec2.png?featherlight=false&width=90pc)
