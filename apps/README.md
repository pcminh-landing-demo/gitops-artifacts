# apps

Put microservices "apps" here along with environment specific values.yaml. No ArgoCD-specific implementations here!

Follow structure
* First level -> Environment: dev, prod, etc...
* Second level -> Deployment Helm Chart: must have respective name under $/charts/*