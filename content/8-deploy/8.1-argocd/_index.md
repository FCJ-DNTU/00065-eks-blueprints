---
title : "Introducing ArgoCD"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 8.1 </b> "
---

#### About ArgoCD

The next step is to use ArgoCD to increase our team’s workload. There are two ways to leverage ArgoCD with EKS Blueprints:

Integrate manual workload onboarding using the ArgoCD CLI and expose the local ArgoCD server to gain access to the dashboard Leverage automated bootstrapping to automate your workload integration.

ArgoCD is a GitOps declarative, continuous delivery tool for Kubernetes. Provisions add Argo CDs to an EKS cluster and optionally launch your workloads from public and private Git repositories.

The Argo CD add-on allows platform administrators to combine cluster provisioning and workload bootstrapping in a single step and enables use cases such as cloning an existing running production cluster in another area for a few minutes. This is critical for business continuity and disaster recovery scenarios as well as availability across regions and geographic expansion.

#### ArgoCD for EKS Blueprints

ArgoCD aligns well with the principles that define the value proposition of using the EKS Blueprint, including:

*   Application definitions, configurations, and environments must be declared and version controlled
*   Application deployment and lifecycle management should be automated, testable, and easy to understand
*   Follow the GitOps model of using Git repositories as a truism to define your desired application state
*   Flexibility in how Kubernetes manifests are defined and managed
*   Argo CD automates the deployment of desired application states in specified target environments. Application deployments can track updates to branches, tags, or be pinned to a specific manifest version at a Git commit.

![Create Workspace](/public/images/8-deploy/8.1-argocd/001-argocd.png?featherlight=false&width=50pc)

Argo CD is implemented as a Kubernetes controller that continuously monitors running applications and compares the current, live state with the desired target state (as specified in the Git repo). Deployed applications whose state directly deviates from the target state is considered out of sync. Argo CD reports & visualizes discrepancies, and provides means to automatically or manually synchronize live state back to the desired target state. Any modifications made to the desired target state in the Git repository can be automatically applied and reflected in the specified target environments.

#### ArgoCD Bootstrapping

EKS Blueprints provides a bootstrap workload approach and add-ons from the customer GitOps repository.

You can see more documentation [Cluster Bootstrapping](https://argo-cd.readthedocs.io/en/stable/operator-manual/cluster-bootstrapping/#app-of-apps-pattern)

To enable bootstrapping, the ArgoCD add-on allows passing an **ApplicationRepository** at build time. Currently, support the following types of repositories:

*   Public HTTP/HTTPS repository (eg GitHub)
*   Git repository accessing Private HTTPS requires username/password authentication.
*   Private git repository with SSH access requires an SSH key for authentication.
*   Private HTTPS accessible GitHub repository is accessible with GitHub token.