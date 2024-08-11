---
title : "Tạo EKS Blueprints"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

#### Tạo EKS Blueprints

Tham khảo cách tạo [Repository Github](https://docs.github.com/en/get-started/quickstart/create-a-repo)

1.  Truy cập vào [New repository](https://github.com/new) của **Github**
    
    *   Trong giao diện **Create a new repository**, nhập **`my-eks-blueprints`** đối với **Repository name**
    *   Chọn **Public**
    *   Chọn **Create repisitory**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0001.png?featherlight=false&width=90pc)

2.  Sau khi tạo **repository** thành công
    
    *   Sao chép và lưu trữ đường dẫn **HTTPS** của **Git repository**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0002.png?featherlight=false&width=90pc)

3.  Trong giao diện **Github** chúng ta sẽ cài đặt và tạo **token**
    
    *   Chọn vào **Avatar** của tài khoản **Github** của bạn
    *   Chọn **Settings**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0003.png?featherlight=false&width=90pc)

4.  Sau đó, kéo xuống và chọn **Developer settings**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0004.png?featherlight=false&width=90pc)

5.  Trong giao diện **Developer settings**
    
    *   Chọn **Personal access tokens**
    *   Chọn **Generate new toke**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0005.png?featherlight=false&width=90pc)

6.  Trong giao diện **Generate new toke**
    
    *   **Note**, nhập **`eks-workshop-toke`**
    *   Chọn các **scope** sau: **repo** và **admin:repo\_hook**
    *   Chọn **Generate token**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0006.png?featherlight=false&width=90pc)

7.  Chọn **Generate token**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0007.png?featherlight=false&width=90pc)

8.  Hoàn thành **Generate token**
    
    *   Sao chép và lưu giữ **token**

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0008.png?featherlight=false&width=90pc)

Tham khảo cách tạo [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

9.  Thực hiện clone **repository**

```
git clone https://github.com/<your-alias>/my-eks-blueprints.git
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/0009.png?featherlight=false&width=90pc)

10.  Thay đổi đường dẫn thư mục.

```
cd ~/environment/my-eks-blueprints
```

![Create EKS Blueprints](/images/3-CreateEKSBlueprints/00010.png?featherlight=false&width=90pc)