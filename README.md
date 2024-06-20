# app-gitops-configs
GitOps for app deployments
## 
## Git secret
- Since Github requires authentication, we need to add [Git creds](https://argo-cd.readthedocs.io/en/latest/operator-manual/declarative-setup/#repository-credentials) to OCP
```
cat <<EOH | oc apply -n argocd -f - 
apiVersion: v1
kind: Secret
metadata:
  name: phammi-repo-creds
  labels:
    argocd.argoproj.io/secret-type: repo-creds
stringData:
  type: git
  url: https://github.wwt.com/phammi
  # Use a personal access token in place of a password.
  password: $GH_WWT_TOKEN
  username: $GH_WWT_USERNAME
EOH
```