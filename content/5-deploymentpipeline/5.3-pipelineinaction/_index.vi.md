---
title : "Pipeline in Action"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 5.3 </b> "
---

#### Pipeline in Action

Các construct đã được sửa đổi, sau đó lưu lại.

1.  Chúng ta thực hiện **add, commit và push** các thay đổi của bạn vào **remote repository**

```
git add .
git commit -m "Setting up EKS Blueprints deployment pipeline"
git branch -M main
git config credential.helper store
git push https://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@github.com/AWS-First-Cloud-Journey/my-eks-blueprints.git
```

*   Vì đây là lần đầu tiên bạn push lên reomte repository của Github, Cloud 9 sẽ nhắc bạn nhập thông tin đăng nhập GitHub của bạn. Bạn sẽ cần sử dụng mật khẩu GitHub của mình (nếu 2FA chưa được bật) hoặc Github Token của bạn (nếu 2FA được bật). Trong bài lab, chúng ta sử dụng **Github Token** vì sử dụng **user name** và **password** đã không còn hiệu lực.
    
*   Nếu quên **Secret** bạn có thể xem trong **AWS Secret Manager**
    
*   Lệnh gọi **credential.helper** dùng để lưu trữ thông tin đăng nhập của bạn để bạn không cần phải tiếp tục nhập chúng mỗi khi thực hiện thay đổi.
    

Lưu ý: git push sử dùng kèm token theo **https://\[token\]@github.com/\[github\_name\]/\[repo\_name\].git**

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/001-pipelineinaction.png?featherlight=false&width=90pc)

2.  Kiểm tra lại repository xem đã được push lên chưa?

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/002-pipelineinaction.png?featherlight=false&width=90pc)

3.  Sau khi push lên repository, chúng ta thực hiện deploy pipeline stack.

```
cdk deploy pipeline-stack
```

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/003-pipelineinaction.png?featherlight=false&width=90pc)

4.  Bạn sẽ được nhắc xác nhận việc triển khai pipeline stack.
    
    *   Nhập **y** và sau đó nhấn enter.
    *   Sau khi triển khai thành công sẽ hiển thị **Stack ARN**

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/004-pipelineinaction.png?featherlight=false&width=90pc)

5.  Quay lại giao diện **AWS Management Console**

*   Tìm và chọn **CodePipeline**

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/005-pipelineinaction.png?featherlight=false&width=90pc)

6.  Bạn sẽ quan sát thấy quá trình triển khai đang diễn ra.

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/006-pipelineinaction.png?featherlight=false&width=90pc)

7.  Đợi khoảng 30 phút sau, **Pipeline** hiển thị **Succeeced**
    
    *   CodePipeline sẽ nhận các thay đổi được thực hiện trong remote repository và pipelne sẽ bắt đầu xây dựng. Bản cập nhật(thêm, xóa, sửa code) có thể được nhìn thấy trong **CodePipeline Console** để xác minh rằng các stage được xây dựng chính xác.
        
    *   Chọn vào tên pipeline.
        

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/007-pipelineinaction.png?featherlight=false&width=90pc)

8.  Xem các bước **Source** và **Build**
    
    *   **Source**: **Source stage** chạy một action để truy xuất các thay đổi code khi pipeline được chạy theo cách thủ công hoặc khi một event webhook được gửi từ source provider. Trong trường hợp của chúng ta, mỗi khi chúng ta thực hiện thay đổi code trong **my-eks-blueprints** repository của mình và reflect những thay đổi trong remote repo, event sẽ được gửi đến pipeline(kèm GitHub personal access token) để kích hoạt thực thi pipline mới.
    *   **Build** : **build stage** cho phép bạn chạy các action test và build như một phần của pipeline.
    *   Trong quá trình **Build**, pipeline sẽ chạy các script để đảm bảo mọi thứ hoạt động như dự định.
    *   Điều này bao gồm **npm package installations**, **version checking** và **CDK synth**.
    *   Bất kỳ lỗi nào trong cấu hình từ repo của bạn đều có thể không thực hiện được stage này.
    *   Bạn có thể xem danh sách các lệnh được chạy trong hành động này bằng cách nhấp vào **Details** trong **actions** (bên dưới tên của nó và **AWS Codebuild**).

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/008-pipelineinaction.png?featherlight=false&width=90pc)

9.  Tiếp theo là **UpdatePipeline** và **Assets**
    
    *   **UpdatePipeline** : Đây là một **extra build stage** chạy để kiểm tra pipeline có cần cập nhật hay không. Ví dụ: nếu code được thay đổi để bao gồm các stage bổ sung (ngoài production), **UpdatePipeline** sẽ chạy build và reconfigure pipeline cần thêm các stage bổ sung đó. Stage này là **Assets** cần thiết để chạy các stage.
    *   **Assets** : Đây là một loạt các build action xử lý các asset cần thiết để triển khai EKS cluster. **Asset**, trong ngữ cảnh của CDK, là các tệp cục bộ, thư mục hoặc Docker image có thể được đóng gói vào các thư viện và ứng dụng CDK. Những nội dung hoặc hiện vật này cần thiết để ứng dụng CDK của chúng ta hoạt động. Các asset này cho phép Framework hoạt động bình thường, vì chúng chứa các tham số và cấu hình được sử dụng để triển khai các tài nguyên cần thiết, tức là Cluster Provider, Kubernetes resources trong Cluster, IAM, add-ons với Helm Charts, v.v. Asset được lưu trữ trên AWS dưới dạng các Lambda Function cho các thực thi và tệp được lưu trữ **S3 Artifacts bucket**.

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/009-pipelineinaction.png?featherlight=false&width=90pc)

10.  Cuối cùng là **dev** (Prepare và Deploy)
    
*   **Envs (our wave)**: wave là một tùy chọn triển khai cho các pipeline cung cấp nhiều stage (hoặc môi trường) song song. Vì CDK tổng hợp code thành một CloudFormation template, bạn có thể xem trong bảng điều khiển quản lý việc triển khai các stack dưới dạng mẫu CloudFormation.

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/010-pipelineinaction.png?featherlight=false&width=90pc)


{{% notice note %}}
Khi mà bạn bị lỗi trong quá trình chạy pipeline thì hãy nhấp vào xem chi tiết
![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/013-pipelineinaction.png?featherlight=false&width=90pc)

Lỗi này là số lượng hàng đợi bị giới hạn.
![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/014-pipelineinaction.png?featherlight=false&height=30pc)

Bạn hãy thực hiện chạy lại
![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/015-pipelineinaction.png?featherlight=false&width=90pc)

Và cuối cùng nó đã chạy được
![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/016-pipelineinaction.png?featherlight=false&width=90pc)
{{% /notice %}}