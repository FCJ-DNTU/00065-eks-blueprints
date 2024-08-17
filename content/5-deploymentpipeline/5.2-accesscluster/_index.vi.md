---
title : "Tạo Pipeline"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 5.2 </b> "
---
#### Tạo Pipeline

#### Thiết lập AWS Secrets Manager

Chúng ta sẽ cần thêm **GitHub Personal Access Token** vào **AWS Secrets Manager** của AWS để tận dụng **AWS CodePipeline** và **GitHub** vì **pipeline** của chúng ta sẽ tận dụng **webhook** để chạy thành công.

Bạn có thể tham khảo thêm về cách tạo [GitHub Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

1.  Sau khi tạo **GitHub Personal Access Token**
    
    *   Chúng ta quay lại **VSCode Terminal**
    *   Thực hiện tạo **Secret trong Secrets Manager** với tên **eks-workshop-token**

```
aws secretsmanager create-secret --name "eks-workshop-token" --description "github access token" --secret-string "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" 
```

Lưu ý: nhớ thay **secret-string** của bạn bằng token bạn đã tạo.

![Create Workspace](/public/images/5-deploymentpipeline/5.2-accesscluster/001-accesscluster.png?featherlight=false&width=90pc)

2.  Chúng ta có thể tạo một tài nguyên **CodePipelineStack** mới bằng cách tạo một **CDK Construct** mới trong thư mục **lib/**, sau đó nhập **Construct** vào main entrypoint file.
    
    *   Thực hiện tạo **construct file** mới.

```
touch lib/pipeline.ts
```

![Create Workspace](/public/images/5-deploymentpipeline/5.2-accesscluster/002-accesscluster.png?featherlight=false&width=90pc)

3.  Sau khi tệp được tạo, hãy mở tệp và thêm đoạn mã sau để tạo **pipeline construct**

```
// lib/pipeline.ts
import * as cdk from 'aws-cdk-lib';
import { Construct } from 'constructs';
import * as blueprints from '@aws-quickstart/eks-blueprints';
import { KubernetesVersion } from 'aws-cdk-lib/aws-eks';

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
          version: 'auto'
        })
      )
      .addOns()
      .teams();

    blueprints.CodePipelineStack.builder()
      .name("eks-blueprints-workshop-pipeline")
      .owner("your-github-username")
      .repository({
          repoUrl: 'your-repo-name',
          credentialsSecretName: 'github-token',
          targetRevision: 'main'
      })
      .build(scope, id+'-stack', props);
  }
}
```

Thực hiện cấu hình:

*   **name**, chúng ta nhập **eks-blueprints-workshop-pipeline** hoặc tên **pipeline** mà bạn muốn.
*   **owner**, nhập tên github của bạn. (trong bài lab, nhập **AWS-First-Cloud-Journey**)
*   **repoUrl**, nhập tên của repo. (Trong bài lab, nhập **my-eks-blueprints**)
*   **credentialsSecretName**, nhập secret của bạn (Trong bài lab, nhập **eks-workshop-token**)
*   **targetRevision**, nhập revision **main**

![Create Workspace](/public/images/5-deploymentpipeline/5.2-accesscluster/003-accesscluster.png?featherlight=false&width=90pc)

4.  Để đảm bảo chúng ta có thể truy cập vào **Construct**, chúng ta cần import và khởi tạo một construct mới.
    
    *   Thay đổi nội dung của file **bin/my-eks-blueprints.ts**

```
// bin/my-eks-blueprints.ts
// bin/my-eks-blueprints.ts
import * as cdk from 'aws-cdk-lib';
import ClusterConstruct from '../lib/my-eks-blueprints-stack';
import * as dotenv from 'dotenv';
import PipelineConstruct from '../lib/pipeline'; // IMPORT OUR PIPELINE CONSTRUCT

dotenv.config();

const app = new cdk.App();
const account = process.env.CDK_DEFAULT_ACCOUNT!;
const region = process.env.CDK_DEFAULT_REGION;
const env = { account, region }

new ClusterConstruct(app, 'cluster', { env });
new PipelineConstruct(app, 'pipeline', { env });
```

![Create Workspace](/public/images/5-deploymentpipeline/5.2-accesscluster/004-accesscluster.png?featherlight=false&width=90pc)

5.  Thực hiện kiểm tra danh sách **pipeline**

```
cdk list
```

![Create Workspace](/public/images/5-deploymentpipeline/5.2-accesscluster/005-accesscluster.png?featherlight=false&width=90pc)

6.  Thực hiện thêm **Stage**. Trong bước này, chúng ta thực hiện thêm các stage cho pipeline( trong bài lab sử dụng stage **dev**, bạn có thể triển khai thêm các stage dành cho **test** và **production** ở các region khác)

```
// lib/pipeline.ts
import * as cdk from 'aws-cdk-lib';
import { Construct } from 'constructs';
import * as blueprints from '@aws-quickstart/eks-blueprints';
import { KubernetesVersion } from 'aws-cdk-lib/aws-eks';

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
          version: 'auto'
        })
      )
      .addOns()
      .teams();

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

*   Sử dụng **class blueprints.StackStage** hỗ trợ tạo để định nghĩa các stage của chúng ta bằng cách sử dụng **.stage**
    
*   Sử dụng **.wave** hỗ trợ để triển khai song song.
    
*   Trong bài lab, chúng ta đang triển khai 1 cluster.
    
*   Nếu trường hợp bạn triển khai nhiều cluster, để giảm thiểu, chúng ta sẽ chỉ cần thêm **.wave** vào danh sách các stage để bao gồm cách bạn muốn cấu trúc các stage triển khai khác nhau của mình trong pipeline. (tức là khác nhau add-ons, region deployment v.v.).
    
*   Stack của chúng ta sẽ triển khai các cluster sau: EKS trong môi trường dev. CodePipeline triển khai tới region: ap-southeast-1.
    

![Create Workspace](/public/images/5-deploymentpipeline/5.2-accesscluster/006-accesscluster.png?featherlight=false&width=90pc)

7.  Thực hiện kiểm tra lại danh sách pipeline

```
cdk list
```

Kết quả như sau:

```
cluster-stack
pipeline-stack
pipeline-stack/dev/dev-blueprint
```

![Create Workspace](/public/images/5-deploymentpipeline/5.2-accesscluster/005-accesscluster.png?featherlight=false&width=90pc)