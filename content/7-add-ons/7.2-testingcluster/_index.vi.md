---
title : "Kiểm tra Cluster Autoscaler"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 7.2 </b> "
---
#### Kiểm tra Cluster Autoscaler

chúng ta đã có thể triển khai Cluster Autoscaler thành công.

Các bước sau sẽ giúp kiểm tra và xác thực chức năng Cluster Autoscaler trong cluster của bạn.

Triển khai một ứng dụng mẫu dưới dạng triển khai. Mở rộng quy mô triển khai lên 50. Giám sát sự kiện mở rộng quy mô.

1.  Triển khai ứng dụng mẫu
    
    *   Kiểm tra số lượng node có sẵn.

```
kubectl get nodes
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/001-testingcluster.png?featherlight=false&width=90pc)

2.  Thực hiện tạo sample nginx application

Tạo thư mục và tạp file `nginx.yaml`
```
mkdir -p /home/ec2-user/environment
sudo vi /home/ec2-user/environment/nginx.yaml
```

Sao chép lệnh này vào nginx.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-to-scaleout
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        service: nginx
        app: nginx
    spec:
      containers:
      - image: nginx
        name: nginx-to-scaleout
        resources:
          limits:
            cpu: 500m
            memory: 512Mi
          requests:
            cpu: 500m
            memory: 512Mi
```

Cuối cùng apply file nginx.yaml
```
kubectl apply -f ~/environment/nginx.yaml
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/002-testingcluster.png?featherlight=false&width=90pc)

3.  Kiểm tra pod đang chạy

```
kubectl get pod -l app=nginx
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/003-testingcluster.png?featherlight=false&width=90pc)

4.  Thực hiện **Scale deployment replicas**

*   Bây giờ chúng ta có thể mở rộng quy mô triển khai lên 10 bản sao và quan sát việc triển khai:

```
kubectl scale --replicas=10 deployment/nginx-to-scaleout
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/004-testingcluster.png?featherlight=false&width=90pc)

5.  Tiếp đến ta thực hiện **Monitoring the scaling event**

*   Một số pod sẽ ở trạng thái Pending, điều này sẽ kích hoạt trình tự động cluster-autoscaler để mở rộng nhóm EC2:

```
kubectl get pods -l app=nginx -o wide --watch
```
![Add-ons](/images/7-add-ons/7.2-testingcluster/005-testingcluster.png?featherlight=false&width=90pc)

6.  Để xem cluster-autoscaler log

```
kubectl -n kube-system logs -f deployment/blueprints-addon-cluster-autoscaler-aws-cluster-autoscaler
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/006-testingcluster.png?featherlight=false&width=90pc)

7.  Bạn có thể liệt kê tất cả các node

```
kubectl get nodes
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/007-testingcluster.png?featherlight=false&width=90pc)

8.  Để xóa tài nguyên thực hiện

```
kubectl delete deploy nginx-to-scaleout
rm ~/environment/nginx.yaml
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/008-testingcluster.png?featherlight=false&width=90pc)