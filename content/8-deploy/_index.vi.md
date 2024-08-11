---
title : "Triển khai Workload với ArgoCD"
date :  "`r Sys.Date()`" 
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---

#### Triển khai Workload với ArgoCD

Giờ đây, bạn đã cấp phép thành công một EKS cluster với các team, role và pipeline của bạn để tự động hóa và quản lý cơ sở hạ tầng. Bước tiếp theo là tận dụng các phương pháp GitOps bằng cách sử dụng ArgoCD để quản lý và tự động hóa workload ứng dụng của chúng ta bằng cách sử dụng các công nghệ và công cụ mà bạn có thể đã quen thuộc như Git.

Trong phần này, chúng ta sẽ trình bày cách tận dụng ArgoCD để triển khai và quản lý workload ứng dụng của chúng ta.

#### ArgoCD là gì?

*   Cách thiết lập và triển khai workload của chúng ta với ArgoCD.
*   Sử dụng giao diện người dùng ArgoCD để quản lý workload đã triển khai.
*   Điều quan trọng là phải hiểu các nguyên tắc chính của GitOps trước khi đi sâu vào phần này.

#### Các nguyên tắc chính của GitOps

*   GitOps là khai báo có nghĩa là một hệ thống được quản lý bằng GitOps phải có trạng thái mong muốn của nó được thể hiện một cách khai báo.
*   Trạng thái mong muốn được lưu trữ theo cách thực thi tính bất biến, lập phiên bản và khôi phục lại lịch sử phiên bản hoàn chỉnh.
*   Tác nhân phần mềm kéo các khai báo trạng thái mong muốn từ nguồn.
*   Các nhân viên của Softare liên tục quan sát trạng thái hệ thống thực tế và cố gắng áp dụng trạng thái mong muốn.

#### Nội dung

1.  [Giới thiệu ArgoCD](8.1-argocd/)
2.  [Triển khai Workload với ArgoCD](8.2-deploy/)
3.  [Quản lý Workload trên ArgoCD](8.3-manage/)