---
title : "Tool Installation"  
date : "`r Sys.Date()`"  
weight : 3  
chapter : false  
pre : " <b> 2.3 </b> "
---

#### Installing kubectl

Amazon EKS clusters require the **kubectl**, **kubelet**, and **aws-cli** or **aws-iam-authenticator** tools to enable IAM authentication for your Kubernetes cluster.

1.  **Install kubectl** by using the following commands:
    
```
sudo curl --silent --location -o /usr/local/bin/kubectl \
   https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl

sudo chmod +x /usr/local/bin/kubectl
```

![Create Workspace](/images/2-prerequiste/2.3-installtool/000-installtool.png?featherlight=false&width=90pc)
    
For more information, refer to the official [AWS guide for installing kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html).
    
2.  **Update awscli** with the following commands:
    

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

![Create Workspace](/images/2-prerequiste/2.3-installtool/002-installtool.png?featherlight=false&width=90pc)

3.  **Verify the installation** by running the following command:

```
for command in kubectl jq envsubst aws
  do
    which $command &>/dev/null && echo "$command in path" || echo "$command NOT FOUND"
  done
```

![Create Workspace](/images/2-prerequiste/2.3-installtool/003-installtool.png?featherlight=false&width=90pc)
    
4.  **Enable kubectl bash completion** with the following commands:
    
```
kubectl completion bash >>  ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
```
![Create Workspace](/images/2-prerequiste/2.3-installtool/004-installtool.png?featherlight=false&width=90pc)