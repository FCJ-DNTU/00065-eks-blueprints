---
title : "Cập nhật IAM"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 2.5 </b> "
---

#### Cập nhật IAM role

Cloud9 sẽ quản lý thông tin chứng thực IAM một cách tự động. Cấu hình mặc định này hiện tại không tương thích với chứng thực EKS thông qua IAM, chúng ta sẽ cần phải vô hiệu hóa tính năng này và sử dụng IAM Role.

1.  Trong giao diện **Cloud9**
    
    *   Chọn **AWS Cloud9**
    *   Chọn **Preferences**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00025.png?featherlight=false&width=90pc)

2.  Trong giao diện **Preferences**
    
    *   Chọn **AWS SETTINGS**
    *   Tắt **AWS managed temporary credentials**
    *   Sau đó, đóng **Preferences** tab

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00026.png?featherlight=false&width=90pc)

3.  Sau khi tắt **AWS managed temporary credentials**
    
    *   Chạy lệnh sau.

```
rm -vf ${HOME}/.aws/credentials
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00027.png?featherlight=false&width=90pc)

4.  Tiến hành cấu hình

```
export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00028.png?featherlight=false&width=90pc)

5.  Kiểm tra **AWS\_REGION**

```
test -n "$AWS_REGION" && echo AWS_REGION is "$AWS_REGION" || echo AWS_REGION is not set
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00029.png?featherlight=false&width=90pc)

6.  Lưu lại vào **bash\_profile**

```
echo "export ACCOUNT_ID=${ACCOUNT_ID}" | tee -a ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" | tee -a ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00030.png?featherlight=false&width=90pc)

7.  Xác thực **IAM role**

```
aws sts get-caller-identity --query Arn | grep eks-blueprints-cdk-workshop-admin -q && echo "IAM role valid" || echo "IAM role NOT valid"
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00031.png?featherlight=false&width=90pc)

Nếu kết quả là IAM role NOT valid, hãy kiểm tra lại các bước trước xem thông tin IAM role bạn tạo và gán vào Cloud9 Workspace có chính xác không nhé.