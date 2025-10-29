# gitops-artifacts

Folder Structure following:

* https://github.com/kostis-codefresh/many-appsets-demo
* https://codefresh.io/blog/how-to-structure-your-argo-cd-repositories-using-application-sets/


The folder structure is as follows:

* /charts/ - consists of Helm charts, no ArgoCD implementations here (i.e., Level 1 in the above article)
* /apps/ - consists of Kubernetes Deployments, also no ArgoCD implementations here (i.e., Level 1 in the above article)
* /argocd/ - consists of ArgoCD implementations (i.e., Level 2 and above in the above article)

So that:

* /charts/ and /apps/ can be deployed manually WITHOUT ArgoCD
* /argocd/ holds the ArgoCD-specific implementations, including Application (following App of Apps pattern) or ApplicationSet


## Prerequisites

### Setup connection to this Repository from the ArgoCD instance

Either using pipeline or manually

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: argocd-gitops-artifact-repo
  namespace: argocd
  labels:
    argocd.argoproj.io/secret-type: repository
stringData:
  type: git
  url: "git@github.com:pcminh-landing-demo/gitops-artifacts.git"
  sshPrivateKey: |
    ${gitops_ssh_private_key_indent_4}
```

### Configure the root Application in the ArgoCD instance

Either using pipeline or manually

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: root-app-${environment}
  namespace: argocd
spec:
  project: default
  source:
    repoURL: git@github.com:pcminh-landing-demo/gitops-artifacts.git
    targetRevision: HEAD
    path: argocd/${environment}
  destination:
    server: https://kubernetes.default.svc
```


