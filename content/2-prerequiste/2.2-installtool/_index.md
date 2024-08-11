---
title : "Install Tool"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Install kubectl

Amazon EKS clusters will need **kubectl** and **kubelet** and **aws-cli** or **aws-iam-authenticator** tools to enable **IAM** authentication for Your **Kubernetes cluster**.

1.  We use the following command to install kubectl.

```
sudo curl --silent --location -o /usr/local/bin/kubectl \
   https://amazon-eks.s3.us-west-2.amazonaws.com/1.21.2/2021-07-05/bin/linux/amd64/kubectl

sudo chmod +x /usr/local/bin/kubectl
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0009.png?featherlight=false&width=90pc)

You can see more installing [kubectl on AWS](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)

2.  Update awscli

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00010.png?featherlight=false&width=90pc)

3.  Install **jq, envsubst (from GNU gettext utilities) and bash-completion**

```
sudo yum -y install jq gettext bash-completion moreutils
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00011.png?featherlight=false&width=90pc)

**jq** is like sed for JSON data - you can use it to slice and filter and map and transform structured data with the same ease as sed, awk, grep.

4.  We perform authentication.

```
for command in kubectl jq envsubst aws
  do
    which $command &>/dev/null && echo "$command in path" || echo "$command NOT FOUND"
  done
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00012.png?featherlight=false&width=90pc)

5.  Enable **kubectl bash\_completion**

```
kubectl completion bash >> ~/.bash_completion
. /etc/profile.d/bash_completion.sh
. ~/.bash_completion
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/00013.png?featherlight=false&width=90pc)