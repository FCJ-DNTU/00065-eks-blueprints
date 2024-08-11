---
title : "Quản lý nhóm bằng IaC"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

#### OnboardTeams

Trong phần này, chúng ta sẽ giới thiệu các nhóm của mình đến EKS Blueprints. chúng ta sẽ xem xét cách tham gia Platform team và Application team cũng như đảm bảo rằng chúng ta đang xác định các cấp quyền truy cập phù hợp cho các nhóm của mình. Một ví dụ là Application team của chúng ta phải có quyền truy cập chỉ đọc vào cơ sở hạ tầng cơ bản và phải được mở rộng phạm vi đến namespace của họ trong khi Platform team của chúng ta sẽ có các cấp độ truy cập chi tiết hơn vì Platform team sẽ chịu trách nhiệm quản lý cơ sở hạ tầng bên dưới.

Lợi ích của việc quản lý nhóm bằng cách sử dụng cơ sở hạ tầng dưới dạng mã (IaC):

*   Mã tự lập tài liệu
*   Logic tập trung liên quan đến nhóm
*   Khả năng sử dụng các template có thể lặp lại để tạo môi trường mới.

#### Nội dung

1.  [OnboardTeams](6.1-definingteams/)
2.  [Onboarding Teams](6.2-onboardingteams/)
3.  [Truy cập Cluster](6.3-clusteraccessforteams/)