---
title : "Manage workloads on ArgoCD"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 8.3 </b> "
---

#### Workload management on ArgoCD

Now, let’s log into the user interface and see how the workloads are being managed through ArgoCD.

1.  By default, the **argocd-server** service is not public. For the purpose of this workshop, we will use the Load Balancer to use.

```
kubectl patch svc blueprints-addon-argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

![Add-ons](/images/8-deploy/8.3-manage/001-manage.png?featherlight=false&width=90pc)

2.  Wait 5 minutes, LoadBalancer is created.

```
export ARGOCD_SERVER=`kubectl get svc blueprints-addon-argocd-server -n argocd -o json | jq --raw-output '.status.loadBalancer.ingress[0].hostname'`
```

![Add-ons](/images/8-deploy/8.3-manage/002-manage.png?featherlight=false&width=90pc)

3.  TYPE and EXTERNAL-IP on argo server service changed to LoadBalancer. Copy the EXTERNAL-IP of LoadBalancer.

```
kubectl get svc -n argocd
```

![Add-ons](/images/8-deploy/8.3-manage/003-manage.png?featherlight=false&width=90pc)

4.  Open a browser and paste the EXTERNAL-IP of **LoadBalancer** in.

![Add-ons](/images/8-deploy/8.3-manage/004-manage.png?featherlight=false&width=90pc)

5.  Implement automatic password generation and username is **admin**

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

![Add-ons](/images/8-deploy/8.3-manage/005-manage.png?featherlight=false&width=90pc)

6.  After logging in, observe the workloads on the ArgoCD UI

![Add-ons](/images/8-deploy/8.3-manage/006-manage.png?featherlight=false&width=90pc)

![Add-ons](/images/8-deploy/8.3-manage/007-manage.png?featherlight=false&width=90pc)