# gitops-artifacts

Folder Structure following:

* https://github.com/kostis-codefresh/many-appsets-demo
* https://codefresh.io/blog/how-to-structure-your-argo-cd-repositories-using-application-sets/


The folder structure is as follows:

* /apps/ - consists of Kubernetes Deployments, no ArgoCD implementations here (i.e., Level 1 in the above article)
* /argocd/ - consists of ArgoCD implementations (i.e., Level 2 and above in the above article)
