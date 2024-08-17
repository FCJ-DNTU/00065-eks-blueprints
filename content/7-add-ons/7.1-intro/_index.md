---
title : "Introducing add-ons"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 7.1 </b> "
---
1.  Adding an add-on to a template is as simple as adding the **.addOns** method to **blueprints.EksBlueprint.builder()**. We will use Cluster Autoscaler as an example to show how simple **add-ons** are using EKS Blueprint. Add **Cluster Autoscaler** to your **lib/pipeline.ts** template as shown below:

```
// lib/pipeline.ts
import * as cdk from 'aws-cdk-lib';
import { Construct } from 'constructs';
import * as blueprints from '@aws-quickstart/eks-blueprints';
import { KubernetesVersion } from 'aws-cdk-lib/aws-eks';
import { TeamApplication, TeamPlatform } from '../teams';

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
          version: KubernetesVersion.V1_29,
        })
      )
      .addOns(new blueprints.ClusterAutoScalerAddOn) // Cluster Autoscaler addon goes here
      .teams(new TeamPlatform(account), new TeamApplication('burnham', account));

    blueprints.CodePipelineStack.builder()
      .name("eks-blueprints-workshop-pipeline")
      .owner("your-github-username")
      .repository({
          repoUrl: 'your-repo-name',
          credentialsSecretName: 'github-token',
          targetRevision: 'main'
      })
      // WE ADD THE STAGES IN WAVE FROM THE PREVIOUS CODE
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

![Add-ons](/public/images/7-add-ons/7.1-intro/001-intro.png?featherlight=false&width=90pc)


2.  If you are new to Cluster Autoscaler, this is a tool that automatically adjusts the number of nodes in your cluster when pods fail due to insufficient resources or pods are rescheduled to other nodes due to failure. used up over a long period. Push your changes to your GitHub repo to start the process.

```
git add .
git commit -m "adding CA"
git push https://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@github.com/AWS-First-Cloud-Journey/my-eks-blueprints.git
```

![Add-ons](/public/images/7-add-ons/7.1-intro/002-intro.png?featherlight=false&width=90pc)

3.  Wait about 15 minutes to complete.

![Add-ons](/public/images/7-add-ons/7.1-intro/003-intro.png?featherlight=false&width=90pc)

4.  Then run the following command to check **Cluster Autoscaler** is running

```
kubectl get pods -n kube-system
```

![Add-ons](/public/images/7-add-ons/7.1-intro/004-intro.png?featherlight=false&width=90pc)