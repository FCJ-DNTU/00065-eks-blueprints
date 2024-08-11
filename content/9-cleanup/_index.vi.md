---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 9 
chapter : false
pre : " <b> 9. </b> "
---

#### Dọn dẹp tài nguyên

1.  Thực hiện xóa **EKS Blueprints**

```
cd ~/environment/my-eks-blueprints
cdk destroy --all
```

![Create Workspace](/images/9-cleanup/0001-cleanup.png?featherlight=false&width=90pc)

2.  Chọn **y**

![Create Workspace](/images/9-cleanup/0002-cleanup.png?featherlight=false&width=90pc)

3.  Truy cập **CloudFormation console** và chọn Stack để cần xóa. Sau đó, chọn **Delete**

![Create Workspace](/images/9-cleanup/0003-cleanup.png?featherlight=false&width=90pc)