---
title : "Add-ons"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
#### Add-ons

Add-ons are third-party (and native AWS) solutions that provide the functionality needed to optimize the efficient running of EKS Blueprints. Add-ons allow you to configure the tools and services you want to run to support your EKS workload. When you configure add-ons for a blueprint, the add-ons are made available at deployment time. Add-ons can deploy both Kubernetes-specific and AWS resources needed to support the add-on functionality.

The benefit of leveraging the EKS Blueprints Add-on is that you extend your ability to leverage open-source projects and tools built by the Kubernetes community. These projects and tools address different areas of running your workload on Kubernetes such as security, observability, CI/CD, GitOps, and more.

| Add-on | Description |
| --- | --- |
| AppMesh | Adds an AppMesh controller and CRDs. |
| ArgoCD | Provisions Argo CD into your cluster. |
| AWS Load Balancer Controlle | Provisions the AWS Load Balancer Controller into your cluster |
| Calico | Adds the Calico 1.7.1 CNI/Network policy engine. |
| Cluster Autoscaler | Adds the standard cluster autoscaler. |
| Container Insights | Adds Container Insights support integrating monitoring with CloudWatch. |
| CoreDNS | Adds CoreDNS (flexible, extensible DNS server) Amazon EKS add-on. |
| ExternalDNS | Adds External DNS support for AWS to the cluster, integrating with Amazon Route 53 |
| Kube Proxy | Adds kube-proxy Amazon EKS add-on (maintains network rules on each Amazon EC2 node). |
| Metrics Server | Adds metrics server (pre-req for HPA and other monitoring tools). |
| Nginx | Adds NGINX ingress controller. |
| Secrets Store | Adds AWS Secrets Manager and Config Provider for Secret Store CSI Driver to the EKS Cluster. |
| SSM Agent | Adds Amazon SSM Agent to worker nodes. |
| VPC CNI | Adds the Amazon VPC CNI Amazon EKS addon to support native VPC networking. |
| Weave GitOps | Weave GitOps Core AddOn. |
| X-Ray | Adds XRay Daemon to the EKS Cluster. |
| OPA Gatekeeper | Adds policy management features to your cluster |
| Velero | Adds Velero to the EKS Cluster. |

#### Content

1.  [Introducing add-ons](7.1-intro/)
2.  [Test Cluster Autotscaler](7.2-testingcluster/)
3.  [Create add-ons](7.3-createaddons/)