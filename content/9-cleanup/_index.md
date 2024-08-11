---
title : "Clean up resources"
date :  "`r Sys.Date()`" 
weight : 9 
chapter : false
pre : " <b> 9. </b> "
---

#### Clean up resources

1.  Perform a delete **EKS Blueprints**

```
cd ~/environment/my-eks-blueprints
cdk destroy --all
```

![Create Workspace](/images/9-cleanup/0001-cleanup.png?featherlight=false&width=90pc)

2.  Select **y**

![Create Workspace](/images/9-cleanup/0002-cleanup.png?featherlight=false&width=90pc)

3.  Go to **CloudFormation console** and select the Stack to delete. Then select **Delete**

![Create Workspace](/images/9-cleanup/0003-cleanup.png?featherlight=false&width=90pc)