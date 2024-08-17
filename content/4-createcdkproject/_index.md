---
title: "Create CDK Project"  
date: "`r Sys.Date()`"  
weight: 4  
chapter: false  
pre: " <b> 4. </b> "
---

#### Create CDK Project

1.  **Change the directory to the main repo and install nvm**
```
cd my-eks-blueprints
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
source ~/.bashrc
nvm -v
```
![Create Workspace](/public/images/4-createcdkproject/001-createcdkproject.png?featherlight=false&width=90pc)

2.  **Use Node.js version 18**
```
nvm install v18
nvm use v18
node -v
npm -v
```
![Create Workspace](/public/images/4-createcdkproject/003-createcdkproject.png?featherlight=false&width=90pc)

{{% notice note %}}
You need to use Node.js version 14.15.0 or higher to use CDK. For more information, see [here](https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html)
![Create Workspace](/public/images/4-createcdkproject/002-createcdkproject.png?featherlight=false&width=90pc)
{{% /notice %}}
    
3.  **Install TypeScript and CDK version 2.147.3**
```
npm -g install typescript
npm install -g aws-cdk@2.147.3
cdk --version
```
![Create Workspace](/public/images/4-createcdkproject/005-createcdkproject.png?featherlight=false&width=90pc)

4.  **Initialize a new CDK project using TypeScript**
    
```
cdk init app --language typescript
```

![Create Workspace](/public/images/4-createcdkproject/006-createcdkproject.png?featherlight=false&width=90pc)
    
5.  **In the VSCode interface**
    *   View the sidebar
    *   Examine the structure of the project
    *   **lib/**: This is where the stacks or constructs of your CDK project are defined. 
    ![Create Workspace](/public/images/4-createcdkproject/012-createcdkproject.png?featherlight=false&width=90pc)
    *   **bin/my-eks-blueprints.ts**: This is the entry point of the CDK project. It will load the constructs defined in **lib/**. 
    ![Create Workspace](/public/images/4-createcdkproject/013-createcdkproject.png?featherlight=false&width=90pc)

{{% notice note %}}  
You can read more about [CDK](https://docs.aws.amazon.com/cdk/v2/guide/best-practices.html).  
{{% /notice %}}
   
6.  **Set the AWS_DEFAULT_REGION and ACCOUNT_ID**
    
```
export AWS_DEFAULT_REGION=ap-southeast-1
export ACCOUNT_ID=212454837823
```
    
{{% notice note %}}  
Note: Remember to replace ACCOUNT_ID with your actual ID for the lab.  
{{% /notice %}}

![Create Workspace](/public/images/4-createcdkproject/007-createcdkproject.png?featherlight=false&width=90pc)
    
7.  **Initialize the bootstrap account**
    
To perform bootstrapping, run:
    
    
```
cdk bootstrap --trust=$ACCOUNT_ID \
  --cloudformation-execution-policies arn:aws:iam::aws:policy/AdministratorAccess \
  aws://$ACCOUNT_ID/$AWS_REGION
```
    
On successful bootstrapping, you will see:
```
Environment aws://212454837823/ap-southeast-1 bootstrapped.
```
    
![Create Workspace](/public/images/4-createcdkproject/010-createcdkproject.png?featherlight=false&width=90pc)
    
8.  **Install the eks-blueprints and dotenv modules for the project**

```
npm i @aws-quickstart/eks-blueprints dotenv
```
    
![Create Workspace](/public/images/4-createcdkproject/011-createcdkproject.png?featherlight=false&width=90pc)