1. Install Argo CD¶
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
References:
1. <https://github.com/argoproj/argocd-example-apps>
2. <https://argo-cd.readthedocs.io/en/stable/getting_started>
