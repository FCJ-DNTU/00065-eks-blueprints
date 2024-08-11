---
title : "Cài đặt Tool"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

#### Cài đặt kubectl

Các cluster của Amazon EKS sẽ cần công cụ **kubectl** và **kubelet** và **aws-cli** hoặc **aws-iam-authenticator** để cho phép chứng thực **IAM** cho **Kubernetes cluster** của bạn.

1.  Chúng ta sử dụng lệnh sau để cài kubectl.

```
sudo curl --silent --location -o /usr/local/bin/kubectl \
   https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl

sudo chmod +x /usr/local/bin/kubectl
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0009.png?featherlight=false&width=90pc)

Các bạn có thể xem thêm cài đặt [kubectl trên AWS](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)

2.  Cập nhật awscli

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00010.png?featherlight=false&width=90pc)

3.  Cài đặt **jq, envsubst (from GNU gettext utilities) và bash-completion**

```
sudo yum -y install jq gettext bash-completion moreutils
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00011.png?featherlight=false&width=90pc)

**jq** giống như sed cho dữ liệu JSON - bạn có thể sử dụng nó để cắt và lọc cũng như ánh xạ và chuyển đổi dữ liệu có cấu trúc với cùng một cách dễ dàng giống như sed, awk, grep.

4.  Chúng ta thực hiện xác thực.

```
for command in kubectl jq envsubst aws
  do
    which $command &>/dev/null && echo "$command in path" || echo "$command NOT FOUND"
  done
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00012.png?featherlight=false&width=90pc)

5.  Kích hoạt **kubectl bash\_completion**

```
kubectl completion bash >>  ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00013.png?featherlight=false&width=90pc)