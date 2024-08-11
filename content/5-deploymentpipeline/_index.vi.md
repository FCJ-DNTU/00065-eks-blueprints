---
title : "Tạo Deployment Pipeline"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

#### Tạo Deployment Pipeline

Trong phần này, chúng ta sẽ xem xét cách thiết lập một deployment pipeline để tự động hóa các bản cập nhật cho cluster của chúng ta. Mặc dù thuận tiện khi tận dụng công cụ dòng lệnh CDK để triển khai stack đầu tiên của bạn, nhung chúng ta nên thiết lập các pipeline tự động chịu trách nhiệm triển khai và cập nhật cơ sở hạ tầng EKS của bạn. Chúng ta sẽ sử dụng **CodePipelineStack** của **Framework** để triển khai môi trường ở các khu vực khác nhau.

**CodePipelineStack** là một cấu trúc để phân phối liên tục các ứng dụng AWS CDK một cách dễ dàng. Bất cứ khi nào bạn kiểm tra mã nguồn của ứng dụng AWS CDK vào GitHub, stack có thể tự động xây dựng, kiểm tra và triển khai phiên bản mới của bạn.

CodePipelineStack tự cập nhật: nếu bạn thêm các stage hoặc stack ứng dụng, pipeline sẽ tự động cấu hình lại chính nó để triển khai các stage hoặc stack mới đó.

#### Nội dung

1.  [Tạo Cluster](5.1-createacluster/)
2.  [Tạo Pipeline](5.2-accesscluster/)
3.  [Pipeline in Action](5.3-pipelineinaction/)
4.  [Truy cập Cluster](5.4-accessingthecluster/)