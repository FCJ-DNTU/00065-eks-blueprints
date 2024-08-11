---
title : "Manage teams using IaC"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

#### OnboardTeams

In this section, we will introduce our teams to EKS Blueprints. we’ll look at how to join a Platform team and an Application team and make sure we’re defining the right access levels for our teams. An example would be that our Application team must have read-only access to the underlying infrastructure and must be extended to their namespace while our Platform team will have granular levels of access. because the Platform team will be responsible for managing the underlying infrastructure.

Benefits of managing teams using infrastructure as code (IaC):

*   Self-documenting code
*   Focused logic related to the group
*   Ability to use repeatable templates to create new environments.

#### Content

1.  [OnboardTeams](6.1-definingteams/)
2.  [Referral group](6.2-onboardingteams/)
3.  [Cluster Access](6.3-clusteraccessforteams/)