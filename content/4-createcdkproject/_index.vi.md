---
title : "Tạo CDK project"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

#### Tạo CDK project

1.  Đầu tiên chúng ta  Thay đổi đường dẫn đến **main repo** và tải nvm
```
cd my-eks-blueprints
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
source ~/.bashrc
nvm -v
```
![Create Workspace](/public/images/4-createcdkproject/001-createcdkproject.png?featherlight=false&width=90pc)

2. Sử dụng phiên bản **node 18**

```
nvm install v18
nvm use v18
node -v
npm -v
```
![Create Workspace](/public/images/4-createcdkproject/003-createcdkproject.png?featherlight=false&width=90pc)

{{% notice note %}}
Bạn cần sử dụng phien bản node trên 14.15.0 để sử dụng được cdk. Xem thêm [tại đây](https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html)
![Create Workspace](/public/images/4-createcdkproject/002-createcdkproject.png?featherlight=false&width=90pc)
{{% /notice %}}


3. Tải Typescript và tải CDK **phiên bản 2.147.3**

```
npm -g install typescript
npm install -g aws-cdk@2.147.3
cdk --version
```
![Create Workspace](/public/images/4-createcdkproject/005-createcdkproject.png?featherlight=false&width=90pc)


4. thực hiện tạo CDK project mới sử dụng typescript

```
cdk init app --language typescript
```

![Create Workspace](/public/images/4-createcdkproject/006-createcdkproject.png?featherlight=false&width=90pc)

5.  Trong giao diện **VSCode**
    *   Xem sidebar
    *   Xem cấu trúc của **project**
    *   **lib /** : Đây là nơi các stack hoặc **construct** **CDK project** của bạn được định nghĩa.
    ![Create Workspace](/public/images/4-createcdkproject/012-createcdkproject.png?featherlight=false&width=90pc)
    *   **bin / my-eks-blueprints.ts** : Đây là **entrypoint** của CDK project. Nó sẽ tải các contructs được định nghĩa trong **lib /** .
    ![Create Workspace](/public/images/4-createcdkproject/013-createcdkproject.png?featherlight=false&width=90pc)

{{% notice note %}}
Bạn có thể xem thêm tài liệu về **[CDK](https://docs.aws.amazon.com/cdk/v2/guide/best-practices.html)**
{{% /notice %}}

6.  Xác thực **AWS\_DEFAULT\_REGION** và **ACCOUNT\_ID**

```
export AWS_DEFAULT_REGION=ap-southeast-1
export ACCOUNT_ID=212454837823
```
{{% notice note %}}
Lưu ý: nhớ thay đổi **ACCOUNT\_ID** của bạn để thực hiện bài lab.
{{% /notice %}}

![Create Workspace](/public/images/4-createcdkproject/007-createcdkproject.png?featherlight=false&width=90pc)

7.  Chúng ta thực hiện khởi tạo **Boostrap account**
    
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

![Create Workspace](/public/images/4-createcdkproject/010-createcdkproject.png?featherlight=false&width=90pc)


8.  Chúng ta tiếp tục chạy lệnh cài đặt module **eks-blueprints** và **dotenv** cho **project**

```
npm i @aws-quickstart/eks-blueprints dotenv
```

![Create Workspace](/public/images/4-createcdkproject/011-createcdkproject.png?featherlight=false&width=90pc)
