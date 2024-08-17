---
title : "Access Cluster"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---
#### Cluster Access

1.  Install access to cluster

```
export KUBE_CONFIG=$(aws cloudformation describe-stacks --stack-name dev-dev-blueprint | jq -r '.Stacks[0].Outputs[] | select(.OutputKey|match("ConfigCommand")))| .OutputValue ')
$KUBE_CONFIG
```
![Create Workspace](/public/images/5-deploymentpipeline/5.4-accessingthecluster/001-accessingthecluster.png?featherlight=false&width=90pc)

2.  Once kubeconfig has been updated, you will be able to access the EKS cluster

```
kubectl get svc
```

![Create Workspace](/public/images/5-deploymentpipeline/5.4-accessingthecluster/002-accessingthecluster.png?featherlight=false&width=90pc)