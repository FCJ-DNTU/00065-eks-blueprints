---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

Bài lab sử dụng các template và quá trình sao chép mã có thể xảy ra lỗi. Tham khảo [Repository](https://github.com/First-Cloud-Journey/my-eks-blueprints) để chỉnh sửa nếu gặp lỗi

#### EKS Blueprints

EKS Blueprints là một khung mã nguồn mở (**open-source development framework**) tóm tắt sự phức tạp của cơ sở hạ tầng đám mây từ các nhà phát triển và cho phép họ triển khai workloads một cách dễ dàng.

Môi trường được chứa trong container trên AWS bao gồm nhiều sản phẩm và dịch vụ AWS hoặc mã nguồn mở, bao gồm các dịch vụ để chạy container, CI/CD pipeline, ghi nhật ký/số liệu và các biện pháp thực thi bảo mật.

EKS Blueprints framework đóng gói các công cụ này thành một tổng thể gắn kết và cung cấp chúng cho các nhóm phát triển như một dịch vụ. Từ góc độ hoạt động, khuôn khổ cho phép các công ty hợp nhất các công cụ và thực tiễn tốt nhất để bảo mật, mở rộng quy mô, giám sát và vận hành cơ sở hạ tầng container thành một nền tảng trung tâm mà sau đó các nhà phát triển trong một doanh nghiệp có thể sử dụng.

![Create Workspace](/public/images/1-introduce/0001-introduce.png?featherlight=false&width=60pc)

#### Hoạt động

EKS Blueprints được xây dựng dựa trên Amazon EKS và tất cả các thành phần khác nhau. EKS Blueprints được định nghĩa thông qua các phương pháp hay nhất về Cơ sở hạ tầng dưới dạng mã (Infrastructre-as-Code) thông qua AWS CDK.

Xem thêm tài liệu về [EKS blueprints dành cho CDK](https://github.com/aws-quickstart/cdk-eks-blueprints) được xây dựng bằng AWS CDK giúp khách hàng dễ dàng xây dựng và triển khai EKS blueprints trên Amazon EKS .

[AWS Cloud Development Kit](https://aws.amazon.com/vi/cdk/) (AWS CDK) là một khung phát triển phần mềm mã nguồn mở để xác định tài nguyên ứng dụng đám mây bằng các ngôn ngữ lập trình quen thuộc.

#### Lợi ích

Khách hàng có thể tận dụng EKS Blueprints để:

*   Triển khai các cluster EKS trên bất kỳ số lượng tài khoản và khu vực nào theo các phương pháp hay nhất.
    
*   Quản lý cấu hình cluster, bao gồm các tiện ích bổ sung chạy trong mỗi cluster, từ một kho lưu trữ Git.
    
*   Xác định nhóm, không gian tên và quyền truy cập liên quan của họ cho các nhóm của bạn.
    
*   Tạo các Continuous Delivery (CD) pipeline chịu trách nhiệm triển khai cơ sở hạ tầng của bạn.
    
*   Tận dụng GitOps-based workflows để giới thiệu và quản lý workload cho nhóm của bạn.
    
*   Các Construct của EKS Blueprints:
    
    *   Bottlerocket
    *   AWS Fargate
    *   Multi-region deployments
    *   Multi-team deployments
    *   Custom cluster deployments

![Create Workspace](/public/images/1-introduce/0003-introduce.png?featherlight=false&width=60pc)