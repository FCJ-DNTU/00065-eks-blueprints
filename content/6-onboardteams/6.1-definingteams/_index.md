---
title : "Setting up teams"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 6.1 </b> "
---

#### Set groups

1.  Implement creating folders as teams including application and platform.

```
mkdir teams && cd teams && mkdir platform-team && mkdir application-team
```

![Deployment Pipeline](/images/5.4-Accesscluster/0003.png?featherlight=false&width=90pc)

2.  We’ll start by creating an IAM user for **platform**.

```
aws iam create-user --user-name platform
```

![Deployment Pipeline](/images/5.4-Accesscluster/0004.png?featherlight=false&width=90pc)

3.  Create a file **index.ts**, used to create resources for **platform-team**

```
cd platform-team && touch index.ts
```

![Deployment Pipeline](/images/5.4-Accesscluster/0005.png?featherlight=false&width=90pc)

4.  Next we add the following code block to **index.ts**

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

Explanation of the code block:

*   The above code block imports **ArnPrincipal construct** from **aws-cdk-lib/aws-iam** module for **AWS CDK** so that users can be added to the platform with IAM credentials their.
    
*   The best way is to extend a class using PlatformTeam class so that our platform/infrastucture people can manage users/roles, while developers can simply create groups using the provided arugments transmisson.
    
*   Then we pass in two arguments: name and list of IAM users.
    

![Deployment Pipeline](/images/5.4-Accesscluster/0006.png?featherlight=false&width=90pc)

#### Application Team

1.  Create **IAM user** for the application team.

```
aws iam create-user --user-name application
```

![Deployment Pipeline](/images/5.4-Accesscluster/0007.png?featherlight=false&width=90pc)

2.  Change directory path and create file **index.ts**

```
cd ../application-team && touch index.ts
```

![Deployment Pipeline](/images/5.4-Accesscluster/0008.png?featherlight=false&width=90pc)

3.  Add code to **teams/application-team/index.ts** file

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

The Application Team template will do the following things:

*   Create a namespace
*   Register quotas
*   Register as an IAM user to access multiple accounts
*   Create a shared role to access the cluster. Alternatively, an existing role can be provisioned.
*   Register the role/user provided in the awsAuth map for kubectl and dashboard access to the cluster and namespace.

![Deployment Pipeline](/images/5.4-Accesscluster/0009.png?featherlight=false&width=90pc)

4.  We will create an additional file **index.ts** in the **team** folder

```
cd .. && touch index.ts
```

![Deployment Pipeline](/images/5.4-Accesscluster/00010.png?featherlight=false&width=90pc)

5.  In the file **index.ts** add the following code:

```
export { TeamPlatform } from './platform-team';
export { TeamApplication } from './application-team';
```

![Deployment Pipeline](/images/5.4-Accesscluster/00011.png?featherlight=false&width=90pc)