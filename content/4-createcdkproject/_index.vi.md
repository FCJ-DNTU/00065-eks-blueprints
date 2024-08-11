---
title : "Tạo CDK project"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

#### Tạo CDK project

1.  Thay đổi đường dẫn đến **main repo** và thực hiện tạo **CDK project** mới sử dụng **typescript**

```
cd ~/environment/my-eks-blueprints
cdk init app --language typescript
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00011.png?featherlight=false&width=90pc)

2.  Trong giao diện **Cloud9 environment**
    
    *   Xem sidebar
    *   Xem cấu trúc của **project**
    *   **lib /** : Đây là nơi các stack hoặc **construct** **CDK project** của bạn được định nghĩa.
    *   **bin / my-eks-blueprints.ts** : Đây là **entrypoint** của CDK project. Nó sẽ tải các contructs được định nghĩa trong **lib /** .

Bạn có thể xem thêm tài liệu về **[CDK](https://docs.aws.amazon.com/cdk/v2/guide/best-practices.html)**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00012.png?featherlight=false&width=90pc)

3.  Xác thực **AWS\_DEFAULT\_REGION** và **ACCOUNT\_ID**

```
export AWS_DEFAULT_REGION=ap-southeast-1
export ACCOUNT_ID=212454837823
```

*   Lưu ý: nhớ thay đổi **ACCOUNT\_ID** của bạn để thực hiện bài lab.

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00013.png?featherlight=false&width=90pc)

4.  Chúng ta thực hiện khởi tạo **Boostrap account**
    
    *   Để **bootstrapping** chúng ta thực hiện lệnh.

```
cdk bootstrap --trust=$ACCOUNT_ID \
  --cloudformation-execution-policies arn:aws:iam::aws:policy/AdministratorAccess \
  aws://$ACCOUNT_ID/$AWS_REGION
```

*   Khi thực hiện **bootstrap** thành công sẽ xuất hiện như sau:

```
Environment aws://212454837823/ap-southeast-1 bootstrapped.
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00014.png?featherlight=false&width=90pc)

5.  Thực hiện cài đặt các dependency.
    
    *   Các dependency cần được cập nhật, mở tệp **package.json** và thay đổi phiên bản của **typescript** lên **4.6.4**
    *   Sau đó, thực hiện cài đặt lại các **package**

```
rm -rf node_modules
npm i
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00015.png?featherlight=false&width=90pc)

6.  Sau khi cài đặt lại đúng version
    
    *   Chúng ta tiếp tục chạy lệnh cài đặt module **eks-blueprints** cho **project**

```
npm i @aws-quickstart/eks-blueprints
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00016.png?featherlight=false&width=90pc)