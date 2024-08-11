---
title : "Tiện ích bổ sung"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
#### Tiện ích bổ sung

Add-ons là các giải pháp của bên thứ ba (và native AWS) cung cấp các chức năng cần thiết để tối ưu hóa việc chạy EKS Blueprints hiệu quả. Add-ons cho phép bạn định cấu hình các công cụ và dịch vụ mà bạn muốn chạy để hỗ trợ EKS workload của bạn. Khi bạn định cấu hình các tiện ích bổ sung cho một blueprint, các tiện ích bổ sung sẽ được cung cấp tại thời điểm triển khai. Tiện ích bổ sung có thể triển khai cả tài nguyên cụ thể của Kubernetes và tài nguyên AWS cần thiết để hỗ trợ chức năng tiện ích bổ sung.

Lợi ích của việc tận dụng Add-on EKS Blueprints là bạn mở rộng khả năng tận dụng các dự án và công cụ nguồn mở do cộng đồng Kubernetes xây dựng. Các dự án và công cụ này giải quyết các lĩnh vực khác nhau của việc chạy workload của bạn trên Kubernetes như bảo mật, khả năng quan sát, CI / CD, GitOps, v.v.

| Add-on | Description |
| --- | --- |
| AppMesh | Adds an AppMesh controller and CRDs. |
| ArgoCD | Provisions Argo CD into your cluster. |
| AWS Load Balancer Controlle | Provisions the AWS Load Balancer Controller into your cluster |
| Calico | Adds the Calico 1.7.1 CNI/Network policy engine. |
| Cluster Autoscaler | Adds the standard cluster autoscaler. |
| Container Insights | Adds Container Insights support integrating monitoring with CloudWatch. |
| CoreDNS | Adds CoreDNS (flexible, extensible DNS server) Amazon EKS add-on. |
| ExternalDNS | Adds External DNS support for AWS to the cluster, integrating with Amazon Route 53 |
| Kube Proxy | Adds kube-proxy Amazon EKS add-on (maintains network rules on each Amazon EC2 node). |
| Metrics Server | Adds metrics server (pre-req for HPA and other monitoring tools). |
| Nginx | Adds NGINX ingress controller. |
| Secrets Store | Adds AWS Secrets Manager and Config Provider for Secret Store CSI Driver to the EKS Cluster. |
| SSM Agent | Adds Amazon SSM Agent to worker nodes. |
| VPC CNI | Adds the Amazon VPC CNI Amazon EKS addon to support native VPC networking. |
| Weave GitOps | Weave GitOps Core AddOn. |
| X-Ray | Adds XRay Daemon to the EKS Cluster. |
| OPA Gatekeeper | Adds policy management features to your cluster |
| Velero | Adds Velero to the EKS Cluster. |

#### Nội dung

1.  [Giới thiệu add-ons](7.1-intro/)
2.  [Kiểm tra Cluster Autotscaler](7.2-testingcluster/)
3.  [Tạo add-ons](7.3-createaddons/)