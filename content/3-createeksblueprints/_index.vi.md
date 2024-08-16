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

![Create Workspace](/images/3-createeksblueprints/001-createeksblueprints.png?featherlight=false&width=90pc)

2.  Sau khi tạo **repository** thành công
    
    *   Sao chép và lưu trữ đường dẫn **HTTPS** của **Git repository**

![Create Workspace](/images/3-createeksblueprints/002-createeksblueprints.png?featherlight=false&width=90pc)

3.  Trong giao diện **Github** chúng ta sẽ cài đặt và tạo **token**
    
    *   Chọn vào **Avatar** của tài khoản **Github** của bạn
    *   Chọn **Settings**
![Create Workspace](/images/3-createeksblueprints/003-createeksblueprints.png?featherlight=false&width=90pc)


4.  Sau đó, kéo xuống và chọn **Developer settings**

![Create Workspace](/images/3-createeksblueprints/004-createeksblueprints.png?featherlight=false&width=90pc)


5.  Trong giao diện **Developer settings**
    
    *   Chọn **Personal access tokens**
    *   Chọn **Generate new toke**

![Create Workspace](/images/3-createeksblueprints/005-createeksblueprints.png?featherlight=false&width=90pc)


6.  Trong giao diện **Generate new token**
    
    *   **Note**, nhập **`eks-workshop-token`**
    *   Chọn các **scope** sau: **repo** và **admin:repo\_hook**
    *   Chọn **Generate token**

![Create Workspace](/images/3-createeksblueprints/006-createeksblueprints.png?featherlight=false&width=90pc)

7.  Chọn **Generate token**

![Create Workspace](/images/3-createeksblueprints/007-createeksblueprints.png?featherlight=false&width=90pc)

8.  Hoàn thành **Generate token**
    
    *   Sao chép và lưu giữ **token**

![Create Workspace](/images/3-createeksblueprints/008-createeksblueprints.png?featherlight=false&width=90pc)

Tham khảo cách tạo [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)


9.  Tải git
```
sudo dnf install git -y
git --version
```

![Create Workspace](/images/3-createeksblueprints/009-createeksblueprints.png?featherlight=false&width=90pc)

10.  Thực hiện clone **repository**

```
git clone https://github.com/<your-alias>/my-eks-blueprints.git
```


![Create Workspace](/images/3-createeksblueprints/010-createeksblueprints.png?featherlight=false&width=90pc)