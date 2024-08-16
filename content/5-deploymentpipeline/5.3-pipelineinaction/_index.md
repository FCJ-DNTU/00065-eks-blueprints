---
title : "Pipeline in Action"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Pipeline in Action

Constructs have been modified, then saved.

1.  We do **add, commit and push** your changes to **remote repository**

```
git add .
git commit -m "Setting up EKS Blueprints deployment pipeline"
git branch -M main
git config credential.helper store
git push https://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@github.com/AWS-First-Cloud-Journey/my-eks-blueprints.git
```

*   Since this is your first time pushing to Github’s repomte repository, Cloud 9 will prompt you to enter your GitHub credentials. You will need to use your GitHub password (if 2FA is not enabled) or your Github Token (if 2FA is enabled). In the lab, we use **Github Token** because using **user name** and **password** is no longer valid.
    
*   If you forgot **Secret** you can view it in **AWS Secret Manager**
    
*   The **credential.helper** call is used to store your credentials so you don’t have to keep entering them every time you make a change.
    

Note: git push uses the accompanying token **https://\[token\]@github.com/\[github\_name\]/\[repo\_name\].git**

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/001-pipelineinaction.png?featherlight=false&width=90pc)


2.  Check if the repository has been pushed up yet?

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/002-pipelineinaction.png?featherlight=false&width=90pc)

3.  After pushing to the repository, we deploy the pipeline stack.

```
cdk deploy pipeline-stack
```

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/003-pipelineinaction.png?featherlight=false&width=90pc)

4.  You will be prompted to confirm the pipeline stack deployment.
    
    *   Type **y** and then press enter.
    *   After successful deployment will display **Stack ARN**

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/004-pipelineinaction.png?featherlight=false&width=90pc)

5.  Return to the **AWS Management Console** interface

*   Find and select **CodePipeline**

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/005-pipelineinaction.png?featherlight=false&width=90pc)

6.  You will see the rollout in progress.

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/006-pipelineinaction.png?featherlight=false&width=90pc)

7.  Wait about 30 minutes, **Pipeline** shows **Succeeced**
    
    *   CodePipeline will pick up the changes made in the remote repository and pipelne will start building. Updates (add, remove, fix code) can be seen in the **CodePipeline Console** to verify that the stages are built correctly.
        
    *   Select the pipeline name.
        

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/007-pipelineinaction.png?featherlight=false&width=90pc)


8.  See **Source** and **Build** steps
    
    *   **Source**: **Source stage** runs an action to retrieve code changes when the pipeline is run manually or when a webhook event is sent from the source provider. In our case, every time we make a code change in our **my-eks-blueprints** repository and reflect the changes in the remote repo, the event will be sent to the pipeline (with GitHub personal access token) ) to enable new pipeline execution.
    *   **Build**: **build stage** allows you to run test and build actions as part of the pipeline.
    *   During **Build**, the pipeline runs scripts to make sure everything works as intended.
    *   This includes **npm package installations**, **version checking** and **CDK synth**.
    *   Any error in the configuration from your repo may make this stage fail.
    *   You can see a list of commands run in this action by clicking **Details** in **actions** (below its name and **AWS Codebuild**).

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/008-pipelineinaction.png?featherlight=false&width=90pc)

9.  Followed by **UpdatePipeline** and **Assets**
    
    *   **UpdatePipeline**: This is an **extra build stage** that runs to check if the pipeline needs updating. For example, if the code is changed to include additional (out-of-production) stages, **UpdatePipeline** will run the build and reconfigure pipeline that needs to add those additional stages. This stage is the **Assets** needed to run the stages.
    *   **Assets**: This is a series of build actions that handle the assets needed to deploy the EKS cluster. **Asset**, in the context of CDK, are local files, directories, or Docker images that can be packaged into CDK libraries and applications. These assets or artifacts are necessary for our CDK application to function. These assets allow the Framework to work properly, as they contain the parameters and configurations used to deploy the necessary resources i.e. Cluster Provider, Kubernetes resources in Cluster, IAM, add-ons with Helm Charts, etc. Assets are stored on AWS as Lambda Functions for **S3 Artifacts bucket** stored files and executables.

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/009-pipelineinaction.png?featherlight=false&width=90pc)

10.  Finally **dev** (Prepare and Deploy)
    
    *   **Envs (our wave)**: a wave is an implementation option for pipelines that provide multiple stages (or environments) in parallel. Because the CDK aggregates code into a CloudFormation template, you can view it in the stack deployment management console as a CloudFormation template.

![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/010-pipelineinaction.png?featherlight=false&width=90pc)


{{% notice note %}}
If you encounter an error during the pipeline execution, click to view the details.
![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/013-pipelineinaction.png?featherlight=false&width=90pc)

This error indicates that the queue limit has been exceeded.
![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/014-pipelineinaction.png?featherlight=false&height=30pc)

You can try retry it.
![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/015-pipelineinaction.png?featherlight=false&width=90pc)

And finally, it should run successfully.
![Create Workspace](/images/5-deploymentpipeline/5.3-pipelineinaction/016-pipelineinaction.png?featherlight=false&width=90pc)
{{% /notice %}}