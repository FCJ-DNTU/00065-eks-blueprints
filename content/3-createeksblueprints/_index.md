---
title : "Create EKS Blueprints"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

#### Create EKS Blueprints

Refer to how to create [Github Repository](https://docs.github.com/en/get-started/quickstart/create-a-repo)

1.  Access to [New repository](https://github.com/new) of **Github**
    
    *   In the **Create a new repository** interface, enter **`my-eks-blueprints`** for **Repository name**
    *   Select **Public**
    *   Select **Create repository**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0001.png?featherlight=false&width=90pc)

2.  After creating **repository** successfully
    
    *   Copy and store **HTTPS** path of **Git repository**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0002.png?featherlight=false&width=90pc)

3.  In the **Github** interface we will install and create **token**
    
    *   Select **Avatar** of your **Github** account
    *   Select **Settings**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0003.png?featherlight=false&width=90pc)

4.  Then scroll down and select **Developer settings**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0004.png?featherlight=false&width=90pc)

5.  In the **Developer settings** interface
    
    *   Select **Personal access tokens**
    *   Select **Generate new token**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0005.png?featherlight=false&width=90pc)

6.  In the **Generate new token** interface
    
    *   **Note**, enter **`eks-workshop-toke`**
    *   Select the following **scope**: **repo** and **admin:repo\_hook**
    *   Select **Generate token**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0006.png?featherlight=false&width=90pc)

7.  Select **Generate token**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0007.png?featherlight=false&width=90pc)

8.  Complete **Generate token**
    
    *   Copy and store **token**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0008.png?featherlight=false&width=90pc)

Refer to how to create [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

9.  Do a clone **repository**

```
git clone https://github.com/<your-alias>/my-eks-blueprints.git
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0009.png?featherlight=false&width=90pc)

10.  Change the directory path.

```
cd ~/environment/my-eks-blueprints
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00010.png?featherlight=false&width=90pc)