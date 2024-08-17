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
import { Construct } from 'constructs';
import * as blueprints from '@aws-quickstart/eks-blueprints';
import { KubernetesVersion } from 'aws-cdk-lib/aws-eks';

import { TeamPlatform, TeamApplication } from '../teams'; // HERE WE IMPORT TEAMS

export default class PipelineConstruct extends Construct {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id)

    const account = props?.env?.account!;
    const region = props?.env?.region!;

    const blueprint = blueprints.EksBlueprint.builder()
      .account(account)
      .region(region)
      .clusterProvider(
        new blueprints.GenericClusterProvider({
          version: 'auto',
        })
      )
      .addOns()
      .teams(new TeamPlatform(account), new TeamApplication('burnham',account)); // HERE WE USE TEAMS

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
          { id: "dev", stackBuilder: blueprint.clone('ap-southeast-1') }
        ]
      })
      .build(scope, id + '-stack', props);
  }
}
```

![Deployment Pipeline](/public/images/6-onboardteams/6.2-onboardingteams/001-onboardingteams.png?featherlight=false&width=90pc)

2.  Push changes to remote repository Github

```
cd ..
git add .
git commit -m "adding teams"
git push https://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@github.com/AWS-First-Cloud-Journey/my-eks-blueprints.git
```

![Deployment Pipeline](/public/images/6-onboardteams/6.2-onboardingteams/002-onboardingteams.png?featherlight=false&width=90pc)

3.  Wait about 15 minutes for **Succeeded**

![Deployment Pipeline](/public/images/6-onboardteams/6.2-onboardingteams/003-onboardingteams.png?featherlight=false&width=90pc)

4.  Successfully deployed
![Deployment Pipeline](/public/images/6-onboardteams/6.2-onboardingteams/004-onboardingteams.png?featherlight=false&width=90pc)

5.  Perform test

```
kubectl get ns
```

*   You will notice that **team-burnham** is in **namespace**

![Deployment Pipeline](/public/images/6-onboardteams/6.2-onboardingteams/005-onboardingteams.png?featherlight=false&width=90pc)