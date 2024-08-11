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

![Onboarding Teams](/images/6.2-OnboardingTeams/0005.png?featherlight=false&width=90pc)

Bạn có thể thấy rằng **Team Burnham** chỉ có thể **get** và **list** một tập hợp các tài nguyên **Kubernetes** tập trung vào ứng dụng (pods, daemonsets, deployments, replicasets, statefulsets, và jobs). Bạn sẽ nhận thấy rằng họ không có quyền create hoặc delete tài nguyên trong namespace tương ứng của họ.

2.  Truy xuất role đã tạo cho Team burnham bằng cách chạy lệnh sau:

```
aws cloudformation describe-stacks --stack-name dev-dev-blueprint | jq -r '.Stacks[0].Outputs[] | select(.OutputKey|match("burnhamteamrole"))| .OutputValue'
```

![Onboarding Teams](/images/6.2-OnboardingTeams/0006.png?featherlight=false&width=90pc)

3.  Tạo thông tin đăng nhập cho **application**

```
aws iam create-login-profile --user-name application --password Ekscdkworkshop123!
```

![Onboarding Teams](/images/6.2-OnboardingTeams/0007.png?featherlight=false&width=90pc)

4.  Truy cập vào [AWS](https://aws.amazon.com/)
    
    *   Thực hiện đăng nhập với **IAM user**
    *   Nhập **Account ID** của bạn
    *   Chọn **Next**

![Onboarding Teams](/images/6.2-OnboardingTeams/0008.png?featherlight=false&width=90pc)

5.  Tiếp theo,
    
    *   Nhập **IAM user name** là **application**
    *   Nhập **password** vừa tạo
    *   Chọn **Sign in**

![Onboarding Teams](/images/6.2-OnboardingTeams/0009.png?featherlight=false&width=90pc)

6.  Hoàn thành đăng nhập

![Onboarding Teams](/images/6.2-OnboardingTeams/00010.png?featherlight=false&width=90pc)

7.  Trong giao diện **AWS**
    
    *   Chọn **Switch role**

![Onboarding Teams](/images/6.2-OnboardingTeams/00011.png?featherlight=false&width=90pc)

8.  Trong giao diện **Switch role**, chọn **Switch Role**

![Onboarding Teams](/images/6.2-OnboardingTeams/00012.png?featherlight=false&width=90pc)

9.  Trong giao diện **Switch Role**
    
    *   **Account**, nhập **Account ID** của bạn
    *   Sau đó, nhập **Role**
    *   Chọn **Switch Role**

![Onboarding Teams](/images/6.2-OnboardingTeams/00013.png?featherlight=false&width=90pc)

10.  Hoàn thành **Switch Role**

![Onboarding Teams](/images/6.2-OnboardingTeams/00014.png?featherlight=false&width=90pc)

11.  Truy cập vào **EKS**

![Onboarding Teams](/images/6.2-OnboardingTeams/00015.png?featherlight=false&width=90pc)

12.  Tại đây, bạn sẽ thấy thông báo lỗi cho biết rằng người dùng Team Burnham KHÔNG được phép liệt kê các triển khai trong tất cả các namespace.

![Onboarding Teams](/images/6.2-OnboardingTeams/00016.png?featherlight=false&width=90pc)

![Onboarding Teams](/images/6.2-OnboardingTeams/00017.png?featherlight=false&width=90pc)

13.  Khi bạn chọn **team-burnham** trong **namespace**, bạn sẽ thấy thông báo bị cấm biến mất. Điều này có nghĩa là bạn hiện đang hiển thị workload của Team Burnham (không có workload nào vì chưa triển khai bất kỳ workload nào).