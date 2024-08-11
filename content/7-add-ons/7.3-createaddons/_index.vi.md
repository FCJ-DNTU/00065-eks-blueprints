---
title : "Tạo add-ons"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 7.3 </b> "
---

#### Tạo add-ons

1.  Đầu tiên, chúng ta tạo **kubevious\_addon.ts** trong thư mục **lib**

```
touch lib/kubevious_addon.ts
```

![Add-ons](/images/7.3-Createaddons/0001.png?featherlight=false&width=90pc)

2.  Thêm đoạn code sau vào file **kubevious\_addon.ts**

```
// lib/kubevious_addon.ts
import { Construct } from 'constructs';
import * as blueprints from '@aws-quickstart/eks-blueprints';
import { setPath } from '@aws-quickstart/eks-blueprints/dist/utils/object-utils';

/**
 * User provided options for the Helm Chart
 */
export interface KubeviousAddOnProps extends blueprints.HelmAddOnUserProps {
  version?: string,
  ingressEnabled?: boolean,
  kubeviousServiceType?: string,
}

/**
 * Default props to be used when creating the Helm chart
 */
const defaultProps: blueprints.HelmAddOnProps & KubeviousAddOnProps = {
  name: "blueprints-kubevious-addon",
  namespace: "kubevious",
  chart: "kubevious",
  version: "0.9.13",
  release: "kubevious",
  repository:  "https://helm.kubevious.io",
  values: {},

  ingressEnabled: false,
  kubeviousServiceType: "ClusterIP",
};

/**
 * Main class to instantiate the Helm chart
 */
export class KubeviousAddOn extends blueprints.HelmAddOn {

  readonly options: KubeviousAddOnProps;

  constructor(props?: KubeviousAddOnProps) {
    super({...defaultProps, ...props});
    this.options = this.props as KubeviousAddOnProps;
  }

  deploy(clusterInfo: blueprints.ClusterInfo): Promise<Construct> {
    let values: blueprints.Values = populateValues(this.options);
    const chart = this.addHelmChart(clusterInfo, values);

    return Promise.resolve(chart);
  }
}

/**
 * populateValues populates the appropriate values used to customize the Helm chart
 * @param helmOptions User provided values to customize the chart
 */
function populateValues(helmOptions: KubeviousAddOnProps): blueprints.Values {
  const values = helmOptions.values ?? {};

  setPath(values, "ingress.enabled",  helmOptions.ingressEnabled);
  setPath(values, "kubevious.service.type",  helmOptions.kubeviousServiceType);
  setPath(values, "mysql.generate_passwords",  true);

  return values;
}
```

![Add-ons](/images/7.3-Createaddons/0002.png?featherlight=false&width=90pc)

3.  Sau đó thêm đoạn code sau vào **lib/pipeline.ts**

```
// lib/pipeline-stack.ts
import * as cdk from 'aws-cdk-lib';
import { Construct } from 'constructs';
import * as blueprints from '@aws-quickstart/eks-blueprints';

import { TeamPlatform, TeamApplication } from '../teams'; 

export default class PipelineConstruct extends Construct {
  constructor(scope: Construct, id: string, props?: cdk.StackProps){
    super(scope,id)

    const blueprint = blueprints.EksBlueprint.builder()
    .account(account)
    .region(region)
    .addOns(
      new blueprints.ClusterAutoScalerAddOn,
      new blueprints.KubeviousAddOn(), // New addon goes here
    ) 
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

![Add-ons](/images/7.3-Createaddons/0003.png?featherlight=false&width=90pc)

4.  Thực hiện push lên Github repository

```
git add .
git commit -m "adding Kubevious"
git push https://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@github.com/AWS-First-Cloud-Journey/my-eks-blueprints.git
```

![Add-ons](/images/7.3-Createaddons/0004.png?featherlight=false&width=90pc)

5.  Đợi 15 phút sau sẽ hoàn thành

![Add-ons](/images/7.3-Createaddons/0005.png?featherlight=false&width=90pc)

6.  Khi pipeline hoàn tất, chúng ta có thể thấy add-ons của mình đang hoạt động bằng cách chạy lệnh bên dưới:

```
kubectl port-forward $(kubectl get pods -n kubevious -l "app.kubernetes.io/component=kubevious-ui" -o jsonpath="{.items[0].metadata.name}") 8080:80 -n kubevious  
```

![Add-ons](/images/7.3-Createaddons/0006.png?featherlight=false&width=90pc)

7.  Trong giao diện **Cloud9**

*   Chọn **Preview**
*   Chọn **Preview Running Application**

![Add-ons](/images/7.3-Createaddons/0007.png?featherlight=false&width=90pc)

8.  Giao diện xuất hiện

*   Chọn vào biểu tượng gốc phải để mở rộng

![Add-ons](/images/7.3-Createaddons/0008.png?featherlight=false&width=90pc)

9.  Giao diện mở rộng

![Add-ons](/images/7.3-Createaddons/0009.png?featherlight=false&width=90pc)

10.  Tiến hành khám phá

![Add-ons](/images/7.3-Createaddons/00010.png?featherlight=false&width=90pc)

11.  Chỉ sử dụng giao diện trên trình duyệt **Desktop**

![Add-ons](/images/7.3-Createaddons/00011.png?featherlight=false&width=90pc)

12.  Giao diện chi tiết của **kubevious**

![Add-ons](/images/7.3-Createaddons/00012.png?featherlight=false&width=90pc)