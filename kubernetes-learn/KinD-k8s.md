#KinD
```
kind version
kind create cluster --name single-node-k8s
kind get clusters
kubectl config current-context
kubectl create deployment nginx --image nginx
kubectl get pods -w
vim multi-node-k8s-cluster.yaml
kind create cluster --name 9-node-k8s --config=multi-node-k8s-cluster.yaml
docker ps | grep -i 9-node-k8s

Expose the application: kubectl port-forward
kubectl create deployment nginx --image nginx
kubectl get pods -w
kubectl port-forward pod/  8989:80
access from browser
localhost:8989
```
You can create a multi node cluster with the following config:

Reference:
1. <https://kind.sigs.k8s.io/>
