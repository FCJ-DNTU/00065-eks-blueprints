---
title: "Session Management"  
date: "`r Sys.Date()`"  
weight: 1  
chapter: false
---

# Introduction to EKS Blueprints

#### Architecture Diagram

![ConnectPrivate](/public/images/1-introduce/0001-introduce.png)

#### Core Concepts

![ConnectPrivate](/public/images/1-introduce/0002-introduce.png)

| Concepts | Description |
| --- | --- |
| Cluster | An EKS Cluster deployed following best practices. |
| Resource Provider | Resource providers are abstractions that supply external AWS resources to the cluster (e.g., hosted zones, VPCs, etc.). |
| Add-on | Allows you to configure, deploy, and update the operational software or add-ons that provide key functionality to support your Kubernetes applications. |
| Teams | A logical grouping of IAM identities that have access to Kubernetes namespaces or cluster administrative access depending upon the team type. |
| Pipelines | Continuous Delivery pipelines for deploying clusters and add-ons |
| Application | An application that runs within an EKS Cluster. |

#### Blueprint

![ConnectPrivate](/public/images/1-introduce/0003-introduce.png)

EKS Blueprints allow you to configure and deploy what is known as a blueprint cluster. A blueprint combines clusters, add-ons, and teams into a cohesive object that can be deployed as a whole. Once the blueprint is configured, it can be easily deployed across any number of AWS accounts and regions. Blueprints also leverage GitOps tools to facilitate cluster bootstrapping and workload integration.

#### Contents

1.  [Introduction](1-introduce/)
2.  [Preparation Steps](2-prerequiste/)
3.  [Creating EKS Blueprints](3-createeksblueprints/)
4.  [Creating CDK Project](4-createcdkproject/)
5.  [Deploying Pipeline](5-deploymentpipeline/)
6.  [Onboarding Teams](6-onboardteams/)
7.  [Add-ons](7-add-ons/)
8.  [Deployment](8-deploy/)
9.  [Cleanup Resources](9-cleanup/)