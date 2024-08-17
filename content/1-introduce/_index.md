---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

#### Overview

The lab uses templates and code duplication is subject to errors. Refer to [Repository](https://github.com/First-Cloud-Journey/my-eks-blueprints) to edit if you get an error

#### EKS Blueprints

EKS Blueprints is an open-source development framework that captures the complexity of cloud infrastructure from developers and enables them to deploy workloads with ease.

Containerized environments on AWS include many open-source or AWS products and services, including services for running containers, CI/CD pipeline, logging/metrics, and security enforcements.

The EKS Blueprints framework packages these tools into a cohesive whole and makes them available to development teams as a service. From an operational perspective, the framework allows companies to unify tools and best practices for securing, scaling, monitoring, and operating container infrastructure into one central platform that developers in an enterprise can use.

![Create Workspace](/public/images/1-introduce/0001-introduce.png?featherlight=false&width=60pc)

#### Work

EKS Blueprints is built on top of Amazon EKS and all the different components. EKS Blueprints are defined through Infrastructure-as-Code best practices through the AWS CDK.

See more documentation on [EKS blueprints for CDK](https://github.com/aws-quickstart/cdk-eks-blueprints) built with AWS CDK making it easy for customers to build and deploy EKS blueprints on Amazon EKS.

[AWS Cloud Development Kit](https://aws.amazon.com/en/cdk/) (AWS CDK) is an open-source software development framework for defining cloud application resources in programming languages and familiar programs.

#### Benefit

Customers can leverage EKS Blueprints to:

*   Deploy EKS clusters on any number of accounts and regions following best practices.
    
*   Manage cluster configuration, including add-ons that run in each cluster, from a single Git repository.
    
*   Define groups, their namespaces, and associated access permissions for your groups.
    
*   Create Continuous Delivery (CD) pipelines responsible for deploying your infrastructure. Leverage GitOps-based workflows to introduce and manage workloads to your team.
    
*   Constructs of EKS Blueprints:
    
    *   Bottlerocket
    *   AWS Fargate
    *   Multi-region deployments
    *   Multi-team deployments
    *   Custom cluster deployments

![Create Workspace](/public/images/1-introduce/0003-introduce.png?featherlight=false&width=60pc)