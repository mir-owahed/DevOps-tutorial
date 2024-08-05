1. Install Argo CD¶
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
Argocd hands-on on minikube
```
minikube start

  303  kubectl get nodes

  304  kubectl get n

  305  kubectl get namespace

  306  kubectl create namespace argocd

  307  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

  308  minikube status

  309  kubectl get pods -n argocd -w

  310  kubectl get svc

  311  kubectl get svc -n argocd

  312  kubectl edit svc argocd-server -n argocd

  313  minikube service list -n argocd

  314  minikube service argocd-server -n argocd
```
```
308  kubectl get secret -n argocd

  309  kubectl edit secret argocd-initial-admin-secret -n argocd

  310  echo cVVTQlBFNm5DV2xhNVJ3Wg== | base64 --decode

  311  kubectl get deployment

  312  kubectl get deploy

  313  curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64

  314  sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd

  315  rm argocd-linux-amd64

```

References:
1. <https://github.com/argoproj/argocd-example-apps>
2. <https://argo-cd.readthedocs.io/en/stable/getting_started>
3. <https://argo-cd.readthedocs.io/en/stable/user-guide/commands/argocd/>
4. <https://argo-cd.readthedocs.io/en/stable/user-guide/commands/argocd_app_create/>
