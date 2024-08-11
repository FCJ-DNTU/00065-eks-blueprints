---
title : "Create Cluster"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

#### Create Cluster

In this section, we will deploy our first EKS cluster using the **eks-blueprints package**. **Blueprints** published as **npm module**

You can learn more about [Amazon EKS Blueprints for CDK](https://www.npmjs.com/package/@aws-quickstart/eks-blueprints)

1.  We edit the main file of **lib/my-eks-blueprints-stack.ts**:
    
    *   Open the file **lib/my-eks-blueprints-stack.ts**
    *   See the sample code in the file

![Deployment Pipeline](/images/5-Deploymentpipeline/0001.png?featherlight=false&width=90pc)

2.  Complete the **lib/my-eks-blueprints-stack.ts** file by pasting (replacing) the following code into the file:

```
// lib/my-eks-blueprints-stack.ts
import * as cdk from 'aws-cdk-lib';
import { Construct } from 'constructs';
import * as blueprints from '@aws-quickstart/eks-blueprints';

export default class ClusterConstruct extends Construct {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id);

    const account = props?.env?.account!;
    const region = props?.env?.region!;

    const blueprint = blueprints.EksBlueprint.builder()
    .account(account)
    .region(region)
    .addOns()
    .teams()
    .build(scope, id+"-stack");
  }
}
```

![Deployment Pipeline](/images/5-Deploymentpipeline/0002.png?featherlight=false&width=90pc)

4.  In this file, we create **CDK Construct** which is the **building block** of the CDK that represents what is needed to build the components of **AWS Cloud**.
    
    *   In our case, the component is the EKS cluster blueprint located in **provided account, region, add-ons, teams** (which we have not assigned), and all other resources needed to create the blueprint( eg VPC, subnet,…). The **build()** command at the end of the cluster blueprint initialization.
        
    *   To make a **construct** usable in the **CDK project**, we need to add it to our **entry point**.
        
    *   Replace the contents of **bin/my-eks-blueprints.ts** with the following **code block**.
        

```
// bin/my-eks-blueprints.ts
import * as cdk from 'aws-cdk-lib';
import ClusterConstruct from '../lib/my-eks-blueprints-stack';


const app = new cdk.App();
const account = process.env.CDK_DEFAULT_ACCOUNT!;
const region = process.env.CDK_DEFAULT_REGION;
const env = { account, region }

new ClusterConstruct(app, 'cluster', { env });
```

![Deployment Pipeline](/images/5-Deploymentpipeline/0004.png?featherlight=false&width=90pc)

5.  Import the Construct file to make it available, then use the CDK app to instantiate a new object of the CDK Construct we imported. Check **CDK**

```
cdk list
```

*   If there are no problems, we have the following result:

```
cluster-stack
```

![Deployment Pipeline](/images/5-Deploymentpipeline/0005.png?featherlight=false&width=90pc)

As you can see, we can leverage EksBlueprint to define our cluster easily using the CDK.

Instead of deploying a single cluster, we’ll leverage the blueprint builder to add a deployment pipeline that can handle all the updates to our infrastructure for the different environments.