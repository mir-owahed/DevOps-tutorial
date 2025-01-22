# install GitLab Runner with the Helm chart
```
helm repo add gitlab https://charts.gitlab.io
```
```
https://gitlab.com/gitlab-org/charts/gitlab-runner/-/tree/main/
```
```
wget https://gitlab.com/gitlab-org/charts/gitlab-runner/-/tree/main/
```
Edit values.yml
```
gitlab url: gitlab.com
registration token:
rbac:
  create : true

rules: 
     - resources: ["events"]
       verbs: ["list", "watch"]
     - resources: ["namespaces"]
    #   verbs: ["create", "delete"]
    # - resources: ["pods"]
    #   verbs: ["create","delete","get"]
    # - apiGroups: [""]
    #   resources: ["pods/attach","pods/exec"]
    #   verbs: ["get","create","patch","delete"]
    # - apiGroups: [""]
    #   resources: ["pods/log"]
    #   verbs: ["get","list"]
    # - resources: ["secrets"]
    #   verbs: ["create","delete","get","update"]
    # - resources: ["serviceaccounts"]
    #   verbs: ["get"]
    # - resources: ["services"]
    #   verbs: ["create","get"]

```
```
helm install --namespace gitlab-runner --create-namespace gitlab-runner -f values.yaml gitlab/gitlab-runner
```
