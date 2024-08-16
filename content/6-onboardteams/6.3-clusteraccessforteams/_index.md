---
title : "Team Access"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 6.3 </b> "
---

#### Group Access

1.  Burnham Team, only having access to resources in their dedicated **namespace** along with a demonstration of how we can use **Kubernative native construct** to ensure that only people used in **team-burnham namespace** can access those resources. This is also known as **soft multi-tenancy** you are using **Kubernetes constructs** like **namespaces**, **quotas**, and **network policies** to prevent applications from being accessed. implementations in different **namespaces** communicate with each other.

```
kubectl describe role -n team-burnham
```

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/001-clusteraccessforteams.png?featherlight=false&width=90pc)

You can see that **Team Burnham** can only **get** and **list** a set of application-focused **Kubernetes** resources (pods, daemonsets, deployments, replicasets, statefulsets, and jobs). You’ll notice that they don’t have permission to create or delete resources in their respective namespaces.

2.  Retrieve the created role for Team burnham by running the following command:

```
aws cloudformation describe-stacks --stack-name dev-dev-blueprint | jq -r '.Stacks[0].Outputs[] | select(.OutputKey|match("burnhamteamrole"))| .OutputValue'
```

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/002-clusteraccessforteams.png?featherlight=false&width=90pc)


3.  Create credentials for **application**

```
aws iam create-login-profile --user-name application --password Ekscdkworkshop123!
```

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/003-clusteraccessforteams.png?featherlight=false&width=90pc)


4.  Go to [AWS](https://aws.amazon.com/)
    
    *   Perform login with **IAM user**
    *   Enter your **Account ID**
    *   Select **Next**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/012-clusteraccessforteams.png?featherlight=false&width=90pc)


5.  Next,
    
    *   Enter **IAM user name** as **application**
    *   Enter **password** just created
    *   Select **Sign in**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/004-clusteraccessforteams.png?featherlight=false&width=90pc)

6.  Complete the login

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/005-clusteraccessforteams.png?featherlight=false&width=90pc)


7.  In the **AWS** interface
    
    *   Select **Switch role**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/006-clusteraccessforteams.png?featherlight=false&width=90pc)


8.  In the **Switch Role** interface
    
    *   **Account**, enter your **Account ID**
    *   Then enter **Role**
    *   Select **Switch Role**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/007-clusteraccessforteams.png?featherlight=false&width=90pc)

9.  Complete **Switch Role**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/008-clusteraccessforteams.png?featherlight=false&width=90pc)

10.  Access to **EKS**

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/009-clusteraccessforteams.png?featherlight=false&width=90pc)

11.  Here you will see an error message stating that the Team Burnham user is NOT allowed to list deployments in all namespaces.

![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/010-clusteraccessforteams.png?featherlight=false&width=90pc)


![Deployment Pipeline](/images/6-onboardteams/6.3-clusteraccessforteams/011-clusteraccessforteams.png?featherlight=false&width=90pc)


12.  When you select **team-burnham** in **namespace**, you will see the forbidden message disappear. This means that you are currently showing Team Burnham workloads (no workloads since any workloads have not been deployed).