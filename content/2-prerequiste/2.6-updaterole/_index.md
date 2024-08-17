---
title : "Update IAM Role"  
date : "`r Sys.Date()`"  
weight : 6  
chapter : false  
pre : " <b> 2.6 </b> "
---

#### Update IAM Role

1.  **Configure the environment**
    
```
export ACCOUNT_ID=xxx
export AWS_REGION=xxx
```
    
![Create Workspace](/images/2-prerequiste/2.6-updaterole/004-updaterole.png?featherlight=false&width=90pc)
    
2.  **Check the `AWS_REGION`**
    
```
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```
    
![Create Workspace](/images/2-prerequiste/2.6-updaterole/005-updaterole.png?featherlight=false&width=90pc)
    
3.  **Save to `bash_profile`**

```
echo "export ACCOUNT_ID=${ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```   
![Create Workspace](/images/2-prerequiste/2.6-updaterole/006-updaterole.png?featherlight=false&width=90pc)
    
4.  **Verify IAM Role**

```
aws sts get-caller-identity --query Arn | grep eks-blueprints-cdk-workshop-admin -q && echo "IAM role valid" || echo "IAM role NOT valid"
```   
    
![Create Workspace](/images/2-prerequiste/2.6-updaterole/007-updaterole.png?featherlight=false&width=90pc)
    

If the result is "IAM role NOT valid," please review the previous steps to ensure that the IAM role you created and assigned to the Cloud9 Workspace is correct.