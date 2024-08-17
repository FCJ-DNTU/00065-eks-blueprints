---
title : "Tạo Cluster"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

#### Tạo Cluster

Trong phần này, chúng ta sẽ triển khai EKS cluster đầu tiên của mình bằng cách sử dụng **eks-blueprints package**. **Blueprints** được xuất bản dưới dạng **mô-đun npm**

Bạn có thể tìm hiểu thêm về [Amazon EKS Blueprints for CDK](https://www.npmjs.com/package/@aws-quickstart/eks-blueprints)

1.  Chúng ta thực hiện chỉnh sửa main file của **lib/my-eks-blueprints-stack.ts**:
    
    *   Mở file **lib/my-eks-blueprints-stack.ts**
    *   Xem các code mẫu trong file

![Deployment Pipeline](/public/images/5-deploymentpipeline/5.1-createacluster/001-createacluster.png?featherlight=false&width=90pc)

2.  Thực hiện hoàn thành file **lib/my-eks-blueprints-stack.ts** bằng cách dán(thay thể) đoạn code sau vào file:

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

![Deployment Pipeline](/public/images/5-deploymentpipeline/5.1-createacluster/002-createacluster.png?featherlight=false&width=90pc)
3.  Chúng ta mở file **bin/my-eks-blueprints.ts** để xem code mẫu.

![Deployment Pipeline](/public/images/5-deploymentpipeline/5.1-createacluster/003-createacluster.png?featherlight=false&width=90pc)
4.  Trong tệp này, chúng ta tạo **CDK Construct** là **building block** của CDK thể hiện những thứ cần thiết để tạo nên các thành phần của **AWS Cloud**.
    
*   Trong trường hợp của chúng ta, thành phần là EKS cluster blueprint đặt trong **provided account, region, add-ons, teams** (mà chúng ta chưa assign) và tất cả các tài nguyên khác cần thiết để tạo blueprint(ví dụ VPC, subnet,…). Lệnh **build()** ở cuối khởi tạo cluster blueprint.
    
*   Để thực sự làm cho một **construct** có thể sử dụng được trong **CDK project**, chúng ta cần thêm nó vào **entrypoint** của chúng ta.
    
*   Thay thế nội dung của **bin/my-eks-blueprints.ts** bằng **code block** sau.
        

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

![Deployment Pipeline](/public/images/5-deploymentpipeline/5.1-createacluster/004-createacluster.png?featherlight=false&width=90pc)

5. Chúng ta tạo mới một file `.env`
![Deployment Pipeline](/public/images/5-deploymentpipeline/5.1-createacluster/005-createacluster.png?featherlight=false&width=90pc)

6. Thêm biên môi trường vào 
```
CDK_DEFAULT_ACCOUNT=XXXXX
CDK_DEFAULT_REGION=XXXX
```
![Deployment Pipeline](/public/images/5-deploymentpipeline/5.1-createacluster/006-createacluster.png?featherlight=false&width=90pc)
{{% notice note %}}
Hãy thay thế bằng **CDK_DEFAULT_ACCOUNT** và **CDK_DEFAULT_REGION** của bạn
{{% /notice %}}


7.  Tệp import Construct để làm cho nó có sẵn, sau đó sử dụng CDK app để khởi tạo một object mới của CDK Construct mà chúng ta đã import. Kiểm tra **CDK**

```
cdk list
```

*   Nếu không có vấn đề, chúng ta có kết quả sau:

```
cluster-stack
```

![Deployment Pipeline](/public/images/5-deploymentpipeline/5.1-createacluster/007-createacluster.png?featherlight=false&width=90pc)

Như bạn có thể thấy, chúng ta có thể tận dụng EksBlueprint để xác định cluster của chúng ta một cách dễ dàng bằng cách sử dụng CDK.

Thay vì triển khai single cluster, chúng ta sẽ tận dụng trình tạo blueprint để thêm deployment pipeline có thể xử lý tất cả các bản cập nhật cho cơ sở hạ tầng của chúng ta cho các môi trường khác nhau.