---
title : "Session Management"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Giới thiệu về EKS Blueprints


#### Sơ đồ kiến trúc

![ConnectPrivate](/images/1-Introduce/0001-introduce.png)

#### Khái niệm cốt lõi

![ConnectPrivate](/images/1-Introduce/0002-introduce.png)

| Concepts          | Description                                                                                                                                              |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cluster           | An EKS Cluster deployed following best practices.                                                                                                        |
| Resource Provider | Resource providers are abstractions that supply external AWS resources to the cluster (e.g. hosted zones, VPCs, etc.).                                   |
| Add-on            | Allow you to configure, deploy, and update the operational software, or add-ons, that provide key functionality to support your Kubernetes applications. |
| Teams             | A logical grouping of IAM identities that have access to a Kubernetes namespace(s), or cluster administrative access depending upon the team type.       |
| Pipelines         | Continuous Delivery pipelines for deploying clusters and add-ons                                                                                         |
| Application       | An application that runs within an EKS Cluster.                                                                                                          |

#### Blueprint

![ConnectPrivate](/images/1-Introduce/0003-introduce.png)

EKS Blueprints cho phép bạn định cấu hình và triển khai những gì gọi là blueprint cluster. Blueprint kết hợp các cluster, tiện ích bổ sung và nhóm thành một đối tượng gắn kết có thể được triển khai tổng thể. Sau khi blueprint được định cấu hình, nó có thể được triển khai dễ dàng trên bất kỳ số lượng tài khoản AWS và khu vực nào. Blueprints cũng tận dụng công cụ GitOps để tạo điều kiện khởi động cluster và tích hợp workload.

#### Nội dung

 1. [Giới thiệu](1-introduce/)
 2. [Các bước chuẩn bị](2-prerequiste/)
 3. [Tạo EKS Blueprints](3-createeksblueprints/)
 4. [Tạo CDK Project](4-createcdkproject/)
 5. [Triển khai Pipeline](5-deploymentpipeline/)
 6. [Onboard Teams](6-onboardteams/)
 7. [Add-ons](7-add-ons/)
 8. [Triển khai](8-deploy/)
 9. [Dọn dẹp tài nguyên](9-cleanup/)
