---
title : "Build Deployment Pipeline"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

#### Building Deployment Pipeline

In this section, we’ll look at how to set up a deployment pipeline to automate updates for our cluster. While it’s convenient to leverage the CDK command-line tool to deploy your first stack, it’s a good idea to set up automated pipelines responsible for deploying and updating your EKS infrastructure. We will use **CodePipelineStack** of **Framework** to deploy environments in different regions.

**CodePipelineStack** is a structure for easy continuous delivery of AWS CDK applications. Whenever you check out the source code of an AWS CDK application on GitHub, the stack can automatically build, test, and deploy your new version.

CodePipelineStack updates itself: if you add stages or application stacks, the pipeline will automatically reconfigure itself to deploy those new stages or stacks.

#### Content

1.  [Create Cluster](5.1-createacluster/)
2.  [Create Pipeline](5.2-accesscluster/)
3.  [Pipeline in Action](5.3-pipelineinaction/)
4.  [Cluster Access](5.4-accessingthecluster/)