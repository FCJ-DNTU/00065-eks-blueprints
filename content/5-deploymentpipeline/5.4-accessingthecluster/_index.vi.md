---
title : ""
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 5.4 </b> "
---
# Truy cập Cluster

#### Truy cập Cluster

1.  Cài đặt quyền truy cập vào cluster

```
export KUBE_CONFIG=$(aws cloudformation describe-stacks --stack-name dev-dev-blueprint | jq -r '.Stacks[0].Outputs[] | select(.OutputKey|match("ConfigCommand"))| .OutputValue')
$KUBE_CONFIG
```

![Deployment Pipeline](/images/5.4-Accesscluster/0001.png?featherlight=false&width=90pc)

2.  Khi kubeconfig đã được cập nhật, bạn sẽ có thể truy cập vào EKS cluster

```
kubectl get svc
```

![Deployment Pipeline](/images/5.4-Accesscluster/0002.png?featherlight=false&width=90pc)