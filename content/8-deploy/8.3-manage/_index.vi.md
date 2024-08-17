---
title : "Quản lý trên ArgoCD"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 8.3 </b> "
---

#### Quản lý workload trên ArgoCD

Bây giờ, chúng ta đăng nhập vào giao diện người dùng và xem cách workloads đang được quản lý thông qua ArgoCD.

1.  Theo mặc định, dịch vụ **argocd-server** không được công khai. Với mục đích của hội thảo này, chúng ta sẽ sử dụng Load Balancer để sử dụng.

```
kubectl patch svc blueprints-addon-argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

![Add-ons](/images/8-deploy/8.3-manage/001-manage.png?featherlight=false&width=90pc)

2.  Đợi 5 phút sau, LoadBalancer được tạo.

```
export ARGOCD_SERVER=`kubectl get svc blueprints-addon-argocd-server -n argocd -o json | jq --raw-output '.status.loadBalancer.ingress[0].hostname'`
```

![Add-ons](/images/8-deploy/8.3-manage/002-manage.png?featherlight=false&width=90pc)

3.  TYPE và EXTERNAL-IP trên argo server service đã thay đổi thành LoadBalancer. Copy EXTERNAL-IP của LoadBalancer.

```
kubectl get svc -n argocd
```

![Add-ons](/images/8-deploy/8.3-manage/003-manage.png?featherlight=false&width=90pc)

4.  Mở trình duyệt và dán EXTERNAL-IP của **LoadBalancer** vào.

![Add-ons](/images/8-deploy/8.3-manage/004-manage.png?featherlight=false&width=90pc)

5.  Thực hiện tạo mật khẩu tự động và username là **admin**

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

![Add-ons](/images/8-deploy/8.3-manage/005-manage.png?featherlight=false&width=90pc)

6.  Sau khi đăng nhập, quan sát các workload trên ArgoCD UI

![Add-ons](/images/8-deploy/8.3-manage/006-manage.png?featherlight=false&width=90pc)

![Add-ons](/images/8-deploy/8.3-manage/007-manage.png?featherlight=false&width=90pc)