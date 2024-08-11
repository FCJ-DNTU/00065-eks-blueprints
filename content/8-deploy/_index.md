---
title : "Deploying Workload with ArgoCD"
date :  "`r Sys.Date()`" 
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---

#### Deploy Workload with ArgoCD

You have now successfully provisioned an EKS cluster with your teams, roles, and pipelines to automate and manage the infrastructure. The next step is to leverage GitOps methodologies using ArgoCD to manage and automate our application workloads using technologies and tools you are probably already familiar with like Git.

In this section, we will demonstrate how to leverage ArgoCD to deploy and manage our application workloads.

#### What is ArgoCD?

*   How to set up and deploy our workload with ArgoCD. Use the ArgoCD user interface to manage deployed workloads.
*   It is important to understand the key principles of GitOps before diving into this section.

#### Key Principles of GitOps

*   GitOps is declarative which means that a system managed with GitOps must have its desired state expressed declaratively.
*   The desired state is stored in a way that enforces immutability, versioning, and restoring a complete version history. The software agent pulls the desired state declarations from the source.
*   Softare employees continuously observe the actual system state and try to apply the desired state.

#### Content

1.  [About ArgoCD](8.1-argocd/)
2.  [Deploy Workload with ArgoCD](8.2-deploy/)
3.  [Workload Management on ArgoCD](8.3-manage/)