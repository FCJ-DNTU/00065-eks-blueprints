---
title : "Cấu hình các nhóm"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 6.2 </b> "
---

#### Cấu hình các nhóm

1.  Trong phần trước, chúng ta tạo cả hai Applicationv à Platform team template.
    
    *   Thêm code sau vào template **// lib/pipeline.ts**

```
// lib/pipeline.ts
import * as cdk from 'aws-cdk-lib';
import * as blueprints from '@aws-quickstart/eks-blueprints';
import { Construct } from 'constructs';

import { TeamPlatform, TeamApplication } from '../teams'; // HERE WE IMPORT TEAMS

export default class PipelineConstruct extends Construct {
  constructor(scope: Construct: string, props?: cdk.StackProps){
    super(scope,id)

    const account = props?.env?.account!;
    const region = props?.env?.region!;
    
    const blueprint = blueprints.EksBlueprint.builder()
    .account(account)
    .region(region)
    .addOns()
    .teams(new TeamPlatform(account), new TeamApplication('burnham',account));
  
    blueprints.CodePipelineStack.builder()
      .name("eks-blueprints-workshop-pipeline")
      .owner("your-github-username")
      .repository({
          repoUrl: 'your-repo-name',
          credentialsSecretName: 'github-token',
          targetRevision: 'main'
      })
      .wave({
        id: "envs",
        stages: [
          { id: "dev", stackBuilder: blueprint.clone('ap-southeast-1')}
        ]
      })
      .build(scope, id+'-stack', props);
  }
}
```

![Onboarding Teams](/images/6.2-OnboardingTeams/0001.png?featherlight=false&width=90pc)

2.  Thực hiện push thay đổi lên remote repository Github

```
cd ..
git add . 
git commit -m "adding teams"
git push https://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@github.com/AWS-First-Cloud-Journey/my-eks-blueprints.git
```

![Onboarding Teams](/images/6.2-OnboardingTeams/0002.png?featherlight=false&width=90pc)

3.  Đợi khoảng thời gian khoảng 15 phút sẽ **Succeeded**

![Onboarding Teams](/images/6.2-OnboardingTeams/0003.png?featherlight=false&width=90pc)

4.  Thực hiện kiểm tra

```
kubectl get ns
```

*   Bạn sẽ nhận thấy rằng **team-burnham** có trong **namespace**

![Onboarding Teams](/images/6.2-OnboardingTeams/0004.png?featherlight=false&width=90pc)