---
title : "Configuring teams"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 6.2 </b> "
---

#### Configure groups

1.  In the previous section, we created both Applications and Platform team templates.
    
    *   Add the following code to the template **// lib/pipeline.ts**

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

2.  Push changes to remote repository Github

```
cd ..
git add .
git commit -m "adding teams"
git push https://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@github.com/AWS-First-Cloud-Journey/my-eks-blueprints.git
```

![Onboarding Teams](/images/6.2-OnboardingTeams/0002.png?featherlight=false&width=90pc)

3.  Wait about 15 minutes for **Succeeded**

![Onboarding Teams](/images/6.2-OnboardingTeams/0003.png?featherlight=false&width=90pc)

4.  Perform test

```
kubectl get ns
```

*   You will notice that **team-burnham** is in **namespace**

![Onboarding Teams](/images/6.2-OnboardingTeams/0004.png?featherlight=false&width=90pc)