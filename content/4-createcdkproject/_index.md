---
title : "Create CDK project"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

#### Create CDK project

1.  Change the path to **main repo** and make a new **CDK project** using **typescript**

```
cd ~/environment/my-eks-blueprints
cdk init app --language typescript
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00011.png?featherlight=false&width=90pc)

2.  In the **Cloud9 environment** interface
    
    *   View sidebar
    *   View structure of **project**
    *   **lib /** : This is where your stack or **construct** **CDK projects** are defined.
    *   **bin / my-eks-blueprints.ts** : This is the **entrypoint** of the CDK project. It will load the constructs defined in **lib /** .

You can see more documentation on **[CDK](https://docs.aws.amazon.com/cdk/v2/guide/best-practices.html)**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00012.png?featherlight=false&width=90pc)

3.  Validate **AWS\_DEFAULT\_REGION** and **ACCOUNT\_ID**

```
export AWS_DEFAULT_REGION=ap-southeast-1
export ACCOUNT_ID=212454837823
```

*   Note: remember to change your **ACCOUNT\_ID** to perform the lab.

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00013.png?featherlight=false&width=90pc)

4.  We initialize **Boostrap account**
    
    *   To **bootstrapping** we execute the command.

```
cdk bootstrap --trust=$ACCOUNT_ID \
  --cloudformation-execution-policies arn:aws:iam::aws:policy/AdministratorAccess \
  aws://$ACCOUNT_ID/$AWS_REGION
```

*   When executing **bootstrap** successfully, the following will appear:

```
Environment aws://212454837823/ap-southeast-1 bootstrapped.
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00014.png?featherlight=false&width=90pc)

5.  Install dependencies.
    
    *   The dependencies need to be updated, open the file **package.json** and change the version of **typescript** to \*\*4.6.
    *   Then do reinstall the **package**

```
rm -rf node_modules
npm i
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00015.png?featherlight=false&width=90pc)

6.  After reinstalling the correct version
    
    *   We continue to run the command to install the **eks-blueprints** module for **project**

```
npm i @aws-quickstart/eks-blueprints
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00016.png?featherlight=false&width=90pc)