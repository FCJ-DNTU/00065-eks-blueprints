---
title : "Kết nối SSH từ Visual Studio Code đến EC2 Instance"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

#### Kết nối SSH từ Visual Studio Code đến EC2 Instance

Kết nối SSH từ Visual Studio Code đến EC2 Instance là giải pháp nhanh chóng thay thế cho việc sử dụng Cloud9.

1.  Chúng ta sẽ tải Visual Studio Code và extensions có tên là **Remote - SSH**

    Bạn có thể tải vs code tại đây: [Download VSCode](https://code.visualstudio.com/download)

    Sau khi tải xong. Chúng ta sẽ tải extension sau đây:
    
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/001-connectec2.png?featherlight=false&width=90pc)
2.  Sau khi tải xong chúng ta nhấn có biểu tượng ở phía dưới góc trái màn hình một hộp thoại sẽ được mở ra.
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/000-connectec2.png?featherlight=false&width=90pc)
3.  Chúng ta sẽ nhấn vào Connect to Host.
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/002-connectec2.png?featherlight=false&width=90pc)
3.  Nhấn vào **Add New SSH Host**.
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/003-connectec2.png?featherlight=false&width=90pc)
4.  Trong ô input nhập **eks-blueprint-remote** và nhấn Enter.
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/004-connectec2.png?featherlight=false&width=90pc)
5.  Nhấn vào đường dẫn trong **C:\Users\ADMIN\.ssh\config** để cấu hình
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/005-connectec2.png?featherlight=false&width=90pc)
6.  Ngay tại khối code SSH name mới được cấu hình trước đó hãy thay đổi thông tin đúng với địa chỉ **IPv4 của EC2 Instance** và đường dẫn đến **Key Pair** trong máy của bạn.  
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/012-connectec2.png?featherlight=false&width=90pc)
7. Bấm vào biểu tượng SSH ở dưới cùng góc bên trái và bắt đầu thực hiện Connect.
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/007-connectec2.png?featherlight=false&width=90pc)
8. Chọn **Continue**
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/009-connectec2.png?featherlight=false&width=90pc)
9. Nhấn vào **Linux**
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/008-connectec2.png?featherlight=false&width=90pc)
10. Chọn **Open Folder** và Click **OK**
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/010-connectec2.png?featherlight=false&width=90pc)
11. Đây là giao diện sau khi kết nối
    ![Create Workspace](/public/images/2-prerequiste/2.2-connectec2/011-connectec2.png?featherlight=false&width=90pc)