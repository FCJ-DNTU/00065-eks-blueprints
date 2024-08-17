---
title : "Cập nhật IAM"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 2.6 </b> "
---

#### Cập nhật IAM role

1.  Tiến hành cấu hình

```
export ACCOUNT_ID=xxx
export AWS_REGION=xxx
```

![Create Workspace](/public/images/2-prerequiste/2.6-updaterole/004-updaterole.png?featherlight=false&width=90pc)

2.  Kiểm tra **AWS\_REGION**

```
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

![Create Workspace](/public/images/2-prerequiste/2.6-updaterole/005-updaterole.png?featherlight=false&width=90pc)

3.  Lưu lại vào **bash\_profile**

```
echo "export ACCOUNT_ID=${ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

![Create Workspace](/public/images/2-prerequiste/2.6-updaterole/006-updaterole.png?featherlight=false&width=90pc)

4.  Xác thực **IAM role**

```
aws sts get-caller-identity --query Arn | grep eks-blueprints-cdk-workshop-admin -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

![Create Workspace](/public/images/2-prerequiste/2.6-updaterole/007-updaterole.png?featherlight=false&width=90pc)

Nếu kết quả là IAM role NOT valid, hãy kiểm tra lại các bước trước xem thông tin IAM role bạn tạo và gán vào Cloud9 Workspace có chính xác không nhé.