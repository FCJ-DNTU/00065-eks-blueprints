---
title : "Testing Cluster Autoscaler"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 7.2 </b> "
---

#### Check Cluster Autoscaler

we were able to deploy Cluster Autoscaler successfully.

The following steps will help test and validate the Cluster Autoscaler functionality in your cluster.

Deploy a sample application as a deployment. Scale deployment to 50. Scaling event monitoring.

1.  Deploy sample application
    
    *   Check the number of available nodes.

```
kubectl get nodes
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/001-testingcluster.png?featherlight=false&width=90pc)

2.  Make sample nginx application
Create a directory and a file named nginx.yaml:
```
mkdir -p /home/ec2-user/environment
sudo vi /home/ec2-user/environment/nginx.yaml
```

Copy the following content into the nginx.yaml file:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-to-scaleout
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        service: nginx
        app: nginx
    spec:
      containers:
      - image: nginx
        name: nginx-to-scaleout
        resources:
          limits:
            cpu: 500m
            memory: 512Mi
          requests:
            cpu: 500m
            memory: 512Mi
```

Finally, apply the nginx.yaml file:
```
kubectl apply -f ~/environment/nginx.yaml
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/002-testingcluster.png?featherlight=false&width=90pc)

3.  Check the pod is running

```
kubectl get pod -l app=nginx
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/003-testingcluster.png?featherlight=false&width=90pc)

4.  Implement **Scale deployment replicas**

*   We can now scale the deployment to 10 replicas and observe the deployment:

```
kubectl scale --replicas=10 deployment/nginx-to-scaleout
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/004-testingcluster.png?featherlight=false&width=90pc)

5.  Next we do **Monitoring the scaling event**

*   Some pods will be in a Pending state, which will trigger the cluster-autoscaler to expand the EC2 pool:

```
kubectl get pods -l app=nginx -o wide --watch
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/005-testingcluster.png?featherlight=false&width=90pc)

6.  To view the cluster-autoscaler log

```
kubectl -n kube-system logs -f deployment/blueprints-addon-cluster-autoscaler-aws-cluster-autoscaler
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/006-testingcluster.png?featherlight=false&width=90pc)

7.  You can list all the nodes

```
kubectl get nodes
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/007-testingcluster.png?featherlight=false&width=90pc)

8.  To delete the execution resource

```
kubectl delete deploy nginx-to-scaleout
rm ~/environment/nginx.yaml
```

![Add-ons](/images/7-add-ons/7.2-testingcluster/008-testingcluster.png?featherlight=false&width=90pc)