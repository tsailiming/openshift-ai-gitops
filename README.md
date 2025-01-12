
# Introduction

This demo shows how GitOps can be used to create OpenShift AI resources.

# Important Disclaimer

> IMPORTANT DISCLAIMER: Read before proceed!
> 1. These examples are to showcase the capabilities of OpenShift AI.
> 1. Certain components may not be supported if they are using upstream projects.
> 1. Always check with Red Hat or your account team for supportability. 

# Requirements

* Tested on OpenShift 4.16 with cluster-admin
* Requires OpenShift AI 2.16 
* OpenShift Service Mesh is installed
* OpenShift Severless is installed
* Authorino is installed
* OpenShift GitOps is installed

# Setup

In OpenShift, I have an [htpasswd](https://docs.openshift.com/container-platform/4.16/authentication/identity_providers/configuring-htpasswd-identity-provider.html) identity provider configured for user1 and user2.

This demo will create an `ApplicationSet` in the `openshift-gitops` namespace. There will be 2 `Application` that manages the resources for each user's namespace. The data science projects will be restricted to individual user.

``` bash
oc apply -f argocd/applicationset.yaml -n openshift-gitops
``` 

This will create 2 datas science projects: user1 and user2 and each with a sample data connection.

You will probably need to sync twice for the `Secret` to be created in the namespace. The namespace has the label `argocd.argoproj.io/managed-by: openshift-gitops`. This creates the role and rolebinding in the new namespace, which allows the Argo CD instance to access and manage resources in it.

# Reference

https://ai-on-openshift.io/odh-rhoai/gitops/


