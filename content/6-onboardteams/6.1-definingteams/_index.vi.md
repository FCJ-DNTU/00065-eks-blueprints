---
title : "Thiết lập các nhóm"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 6.1 </b> "
---

#### Thiết lập các nhóm

1.  Thực hiện tạo các thư mục là các team gồm: application và platform.

```
mkdir teams && cd teams && mkdir platform-team && mkdir application-team
```

![Deployment Pipeline](/images/5.4-Accesscluster/0003.png?featherlight=false&width=90pc)

2.  Chúng ta sẽ bắt đầu bằng cách tạo một IAM user cho **platform**.

```
aws iam create-user --user-name platform
```

![Deployment Pipeline](/images/5.4-Accesscluster/0004.png?featherlight=false&width=90pc)

3.  Tạo một file **index.ts**, dùng để tạo ressource cho **platform-team**

```
cd platform-team && touch index.ts
```

![Deployment Pipeline](/images/5.4-Accesscluster/0005.png?featherlight=false&width=90pc)

4.  Tiếp theo chúng ta thêm code block sau vào **index.ts**

```
import { ArnPrincipal } from "aws-cdk-lib/aws-iam";
import { PlatformTeam } from '@aws-quickstart/eks-blueprints';

export class TeamPlatform extends PlatformTeam {
    constructor(accountID: string) {
        super({
            name: "platform",
            users: [new ArnPrincipal(`arn:aws:iam::${accountID}:user/platform`)]
        })
    }
}
```

Giải thích đoạn code block:

*   Code block ở trên nhập **ArnPrincipal construct** từ mô-đun **aws-cdk-lib/aws-iam** cho **AWS CDK** để có thể thêm người dùng vào platform bằng thông tin đăng nhập IAM của họ.
    
*   Cách tốt nhất là mở rộng một class bằng cách sử dụng PlatformTeam class để những người thuộc platform/infrastucture của chúng ta có thể quản lý users/roles, trong khi các developer có thể chỉ cần tạo group bằng cách sử dụng các arugments được truyền vào.
    
*   Sau đó, chúng ta chuyển vào hai arugment: name và danh sách IAM user.
    

![Deployment Pipeline](/images/5.4-Accesscluster/0006.png?featherlight=false&width=90pc)

#### Application Team

1.  Thực hiện tạo **IAM user** cho application team.

```
aws iam create-user --user-name application
```

![Deployment Pipeline](/images/5.4-Accesscluster/0007.png?featherlight=false&width=90pc)

2.  Thay đổi đường dẫn thư mục và tạo file **index.ts**

```
cd ../application-team && touch index.ts
```

![Deployment Pipeline](/images/5.4-Accesscluster/0008.png?featherlight=false&width=90pc)

3.  Thêm code vào **teams/application-team/index.ts** file

```
import { ArnPrincipal } from 'aws-cdk-lib/aws-iam';
import { ApplicationTeam } from '@aws-quickstart/eks-blueprints';


export class TeamApplication extends ApplicationTeam {
    constructor(name: string, accountID: string) {
        super({
            name: name, 
            users: [new ArnPrincipal(`arn:aws:iam::${accountID}:user/application`)] 
        });
    }
}
```

Application Team template sẽ thực hiện những việc sau:

*   Tạo một namespace
*   Register quotas
*   Đăng ký người dùng IAM để truy cập nhiều tài khoản
*   Tạo một role được chia sẻ để truy cập cluster. Ngoài ra, một role hiện có có thể được cung cấp.
*   Đăng ký role/user được cung cấp trong awsAuth map để truy cập kubectl và bảng điều khiển vào cluster và namespace.

![Deployment Pipeline](/images/5.4-Accesscluster/0009.png?featherlight=false&width=90pc)

4.  Chúng ta sẽ tạo thêm file **index.ts** trong thư mục **team**

```
cd .. && touch index.ts
```

![Deployment Pipeline](/images/5.4-Accesscluster/00010.png?featherlight=false&width=90pc)

5.  Trong file **index.ts** thêm code sau vào:

```
export { TeamPlatform } from './platform-team';
export { TeamApplication } from './application-team';
```

![Deployment Pipeline](/images/5.4-Accesscluster/00011.png?featherlight=false&width=90pc)