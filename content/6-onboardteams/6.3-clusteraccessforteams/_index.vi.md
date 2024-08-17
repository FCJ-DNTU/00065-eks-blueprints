---
title : "Quyền truy cập nhóm"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 6.3 </b> "
---

#### Quyền truy cập nhóm

1.  Burnham Team, chỉ có quyền truy cập vào các tài nguyên trong **namespace** dành riêng của họ cùng với việc chứng minh cách chúng ta có thể sử dụng **Kubernative native construct** để đảm bảo rằng chỉ những người dùng trong **team-burnham namespace** có thể truy cập các tài nguyên đó. Đây còn được gọi là **soft multi-tenancy** bạn đang sử dụng các **Kubernetes constructs** như **namespaces**, **quotas**, và **network policies** để ngăn các ứng dụng được triển khai trong các **namespace** khác nhau giao tiếp với nhau.

```
kubectl describe role -n team-burnham
```

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/001-clusteraccessforteams.png?featherlight=false&width=90pc)


Bạn có thể thấy rằng **Team Burnham** chỉ có thể **get** và **list** một tập hợp các tài nguyên **Kubernetes** tập trung vào ứng dụng (pods, daemonsets, deployments, replicasets, statefulsets, và jobs). Bạn sẽ nhận thấy rằng họ không có quyền create hoặc delete tài nguyên trong namespace tương ứng của họ.

2.  Truy xuất role đã tạo cho Team burnham bằng cách chạy lệnh sau:

```
aws cloudformation describe-stacks --stack-name dev-dev-blueprint | jq -r '.Stacks[0].Outputs[] | select(.OutputKey|match("burnhamteamrole"))| .OutputValue'
```

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/002-clusteraccessforteams.png?featherlight=false&width=90pc)


3.  Tạo thông tin đăng nhập cho **application**

```
aws iam create-login-profile --user-name application --password Ekscdkworkshop123!
```

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/003-clusteraccessforteams.png?featherlight=false&width=90pc)


4.  Truy cập vào [AWS](https://aws.amazon.com/)
    
    *   Thực hiện đăng nhập với **IAM user**
    *   Nhập **Account ID** của bạn
    *   Chọn **Next**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/012-clusteraccessforteams.png?featherlight=false&width=90pc)


5.  Tiếp theo,
    
    *   Nhập **IAM user name** là **application**
    *   Nhập **password** vừa tạo
    *   Chọn **Sign in**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/004-clusteraccessforteams.png?featherlight=false&width=90pc)

6.  Hoàn thành đăng nhập

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/005-clusteraccessforteams.png?featherlight=false&width=90pc)


7.  Trong giao diện **AWS**
    
    *   Chọn **Switch role**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/006-clusteraccessforteams.png?featherlight=false&width=90pc)

8.  Trong giao diện **Switch Role**
    
    *   **Account**, nhập **Account ID** của bạn
    *   Sau đó, nhập **Role**
    *   Chọn **Switch Role**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/007-clusteraccessforteams.png?featherlight=false&width=90pc)


9.  Hoàn thành **Switch Role**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/008-clusteraccessforteams.png?featherlight=false&width=90pc)


10.  Truy cập vào **EKS**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/009-clusteraccessforteams.png?featherlight=false&width=90pc)

11.  Tại đây, bạn sẽ thấy thông báo lỗi cho biết rằng người dùng Team Burnham KHÔNG được phép liệt kê các triển khai trong tất cả các namespace.

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/012-clusteraccessforteams.png?featherlight=false&width=90pc)

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/011-clusteraccessforteams.png?featherlight=false&width=90pc)

12.  Khi bạn chọn **team-burnham** trong **namespace**, bạn sẽ thấy thông báo bị cấm biến mất. Điều này có nghĩa là bạn hiện đang hiển thị workload của Team Burnham (không có workload nào vì chưa triển khai bất kỳ workload nào).