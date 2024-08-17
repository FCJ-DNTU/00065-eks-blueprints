---
title : "Cài đặt Tool"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---

#### Cài đặt kubectl

Các cluster của Amazon EKS sẽ cần công cụ **kubectl** và **kubelet** và **aws-cli** hoặc **aws-iam-authenticator** để cho phép chứng thực **IAM** cho **Kubernetes cluster** của bạn.

1.  Chúng ta sử dụng lệnh sau để cài kubectl.

```
sudo curl --silent --location -o /usr/local/bin/kubectl \
   https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl

sudo chmod +x /usr/local/bin/kubectl
```

![Create Workspace](/public/images/2-prerequiste/2.3-installtool/000-installtool.png?featherlight=false&width=90pc)
Các bạn có thể xem thêm cài đặt [kubectl trên AWS](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)

2.  Cập nhật awscli

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

![Create Workspace](/public/images/2-prerequiste/2.3-installtool/002-installtool.png?featherlight=false&width=90pc)

3.  Chúng ta thực hiện xác thực.

```
for command in kubectl jq envsubst aws
  do
    which $command &>/dev/null && echo "$command in path" || echo "$command NOT FOUND"
  done
```

![Create Workspace](/public/images/2-prerequiste/2.3-installtool/003-installtool.png?featherlight=false&width=90pc)

4.  Kích hoạt **kubectl bash\_completion**

```
kubectl completion bash >>  ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
```
![Create Workspace](/public/images/2-prerequiste/2.3-installtool/004-installtool.png?featherlight=false&width=90pc)
