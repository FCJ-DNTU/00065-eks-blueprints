---
title : "Giới thiệu ArgoCD"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 8.1 </b> "
---

#### Giới thiệu ArgoCD

Bước tiếp theo là sử dụng ArgoCD để tăng workload của nhóm chúng ta. Có hai cách để tận dụng ArgoCD với EKS Blueprints:

*   Tích hợp workload onboarding thủ công bằng ArgoCD CLI và hiển thị ArgoCD server cục bộ để có quyền truy cập vào bảng điều khiển
    
*   Tận dụng bootstrapping tự động để tự động hóa việc tích hợp workload của bạn.
    
*   CD Argo là một công cụ phân phối liên tục, mang tính khai báo GitOps cho Kubernetes. Các điều khoản bổ sung Argo CD vào một cluster EKS và có thể tùy chọn khởi động khối lượng công việc của bạn từ các kho lưu trữ Git công khai và riêng tư.
    
*   Tiện ích bổ sung Argo CD cho phép quản trị viên nền tảng kết hợp cung cấp cluster và khởi động khối lượng công việc trong một bước duy nhất và cho phép các trường hợp sử dụng như sao chép một cluster sản xuất đang chạy hiện có ở một khu vực khác trong vài phút. Điều này rất quan trọng đối với tính liên tục của hoạt động kinh doanh và các trường hợp khắc phục thảm họa cũng như tính khả dụng giữa các khu vực và mở rộng địa lý.
    

#### ArgoCD cho EKS Blueprints

ArgoCD phù hợp tốt với các nguyên tắc xác định đề xuất giá trị của việc sử dụng Bản thiết kế EKS, bao gồm:

*   Các định nghĩa, cấu hình và môi trường ứng dụng phải được khai báo và kiểm soát phiên bản
*   Việc triển khai ứng dụng và quản lý vòng đời phải được tự động hóa, có thể kiểm tra được và dễ hiểu
*   Tuân theo mô hình GitOps sử dụng kho lưu trữ Git như một chân lý để xác định trạng thái ứng dụng mong muốn của bạn
*   Tính linh hoạt về cách Kubernetes biểu hiện được xác định và quản lý
*   Argo CD tự động hóa việc triển khai các trạng thái ứng dụng mong muốn trong các môi trường đích được chỉ định. Việc triển khai ứng dụng có thể theo dõi các bản cập nhật cho các nhánh, thẻ hoặc được ghim vào một phiên bản tệp kê khai cụ thể tại một cam kết Git.

![Create Workspace](/public/images/8-deploy/8.1-argocd/001-argocd.png?featherlight=false&width=50pc)

Argo CD được thực hiện như một bộ điều khiển Kubernetes liên tục theo dõi các ứng dụng đang chạy và so sánh trạng thái hiện tại, trực tiếp với trạng thái mục tiêu mong muốn (như được chỉ định trong Git repo). Ứng dụng đã triển khai có trạng thái trực tiếp lệch khỏi trạng thái đích được coi là OutOfSync. Argo CD báo cáo & trực quan hóa sự khác biệt, đồng thời cung cấp các phương tiện để tự động hoặc thủ công đồng bộ hóa trạng thái trực tiếp trở lại trạng thái mục tiêu mong muốn. Bất kỳ sửa đổi nào được thực hiện đối với trạng thái mục tiêu mong muốn trong kho Git có thể được tự động áp dụng và phản ánh trong các môi trường mục tiêu được chỉ định.

#### ArgoCD Bootstrapping

EKS Blueprints cung cấp cách tiếp cận bootstrap workload và add-ons từ customer GitOps repository.

Bạn xem thêm tài liệu [Cluster Bootstrapping](https://argo-cd.readthedocs.io/en/stable/operator-manual/cluster-bootstrapping/#app-of-apps-pattern)

Để cho phép bootstrapping, ArgoCD add-on cho phép chuyển một **ApplicationRepository** thời điểm xây dựng. Hiện tại hỗ trợ các loại repository sau:

*   Public HTTP/HTTPS repository (ví dụ: GitHub)
*   Git repository truy cập Private HTTPS yêu cầu xác thực tên người dùng / mật khẩu.
*   Private git repository với quyền truy cập SSH yêu cầu SSH key để xác thực.
*   GitHub repository có thể truy cập Private HTTPS có thể truy cập được bằng GitHub token.