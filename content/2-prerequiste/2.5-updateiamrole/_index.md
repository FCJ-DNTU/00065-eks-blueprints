---
title : "Install Tool"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.5 </b> "
---

# Update IAM role

#### Update IAM role

Cloud9 will manage IAM credentials automatically. This default configuration is currently not compatible with EKS authentication via IAM, we will need to disable this feature and use the IAM Role.

1.  In the **Cloud9** interface
    
    *   Select **AWS Cloud9**
    *   Select **Preferences**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00025.png?featherlight=false&width=90pc)

2.  In the **Preferences** interface
    
    *   Select **AWS SETTINGS**
    *   Turn off **AWS managed temporary credentials**
    *   Then close **Preferences** tab

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00026.png?featherlight=false&width=90pc)

3.  After turning off **AWS managed temporary credentials**
    
    *   Run the following command.

```
rm -vf ${HOME}/.aws/credentials
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00027.png?featherlight=false&width=90pc)

4.  Proceed to configure

```
export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00028.png?featherlight=false&width=90pc)

5.  Check **AWS\_REGION**

```
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00029.png?featherlight=false&width=90pc)

6.  Save to **bash\_profile**

```
echo "export ACCOUNT_ID=${ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00030.png?featherlight=false&width=90pc)

7.  Authentication **IAM role**

```
aws sts get-caller-identity --query Arn | grep eks-blueprints-cdk-workshop-admin -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00031.png?featherlight=false&width=90pc)

If the result is IAM role NOT valid, please check the previous steps to see if the IAM role information you created and assigned to Cloud9 Workspace is correct.