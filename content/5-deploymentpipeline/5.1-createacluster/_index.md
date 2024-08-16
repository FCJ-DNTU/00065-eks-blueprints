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

![Deployment Pipeline](/images/5-deploymentpipeline/5.1-createacluster/001-createacluster.png?featherlight=false&width=90pc)

2.  Complete the **lib/my-eks-blueprints-stack.ts** file by pasting (replacing) the following code into the file:

```
// lib/my-eks-blueprints-stack.ts
import * as cdk from 'aws-cdk-lib';
import { Construct } from 'constructs';
import * as blueprints from '@aws-quickstart/eks-blueprints';
import { KubernetesVersion } from 'aws-cdk-lib/aws-eks';

export default class ClusterConstruct extends Construct {
  constructor(scope: Construct, id: string, props?: cdk.StackProps) {
    super(scope, id);

    const account = props?.env?.account!;
    const region = props?.env?.region!;

    const blueprint = blueprints.EksBlueprint.builder()
      .account(account)
      .region(region)
      .clusterProvider(
        new blueprints.GenericClusterProvider({
          version: 'auto'
        })
      )
      .addOns()
      .teams()
      .build(scope, id + "-stack");
  }
}
```

![Deployment Pipeline](/images/5-deploymentpipeline/5.1-createacluster/002-createacluster.png?featherlight=false&width=90pc)

3.  Open the file **bin/my-eks-blueprints.ts** to review the sample code.

![Deployment Pipeline](/images/5-deploymentpipeline/5.1-createacluster/003-createacluster.png?featherlight=false&width=90pc)

4.  In this file, we create a **CDK Construct**, which is a **building block** of CDK representing what is necessary to create components of **AWS Cloud**.
    
    *   In our case, the component is an EKS cluster blueprint placed in **provided account, region, add-ons, teams** (which we haven't assigned yet) and all other resources necessary to create the blueprint (e.g., VPC, subnet, etc.). The **build()** command at the end initializes the cluster blueprint.
        
    *   To actually make a **construct** usable in a **CDK project**, we need to add it to our **entrypoint**.
        
    *   Replace the contents of **bin/my-eks-blueprints.ts** with the following **code block**.
        

```
// bin/my-eks-blueprints.ts
import * as cdk from 'aws-cdk-lib';
import ClusterConstruct from '../lib/my-eks-blueprints-stack';
import * as dotenv from 'dotenv';

const app = new cdk.App();
const account = process.env.CDK_DEFAULT_ACCOUNT!;
const region = process.env.CDK_DEFAULT_REGION;
const env = { account, region }

new ClusterConstruct(app, 'cluster', { env });
```

![Deployment Pipeline](/images/5-deploymentpipeline/5.1-createacluster/004-createacluster.png?featherlight=false&width=90pc)

5.  Create a new **.env** file.

![Deployment Pipeline](/images/5-deploymentpipeline/5.1-createacluster/005-createacluster.png?featherlight=false&width=90pc)

6.  Add environment variables:

```
CDK_DEFAULT_ACCOUNT=XXXXX
CDK_DEFAULT_REGION=XXXX
```

![Deployment Pipeline](/images/5-deploymentpipeline/5.1-createacluster/006-createacluster.png?featherlight=false&width=90pc)

{{% notice note %}} 
Please replace **CDK\_DEFAULT\_ACCOUNT** and **CDK\_DEFAULT\_REGION** with your own values. {{% /notice %}}

7.  Import Construct to make it available, then use the CDK app to initialize a new object of the CDK Construct we imported. Check **CDK**:

```
cdk list
```

*   If there are no issues, you should see the following result:


```
cluster-stack
```

![Deployment Pipeline](/images/5-deploymentpipeline/5.1-createacluster/007-createacluster.png?featherlight=false&width=90pc)

As you can see, we can leverage EksBlueprint to define our cluster easily using CDK.

Instead of deploying a single cluster, we will utilize the blueprint generator to add a deployment pipeline that can handle all updates for our infrastructure across different environments.