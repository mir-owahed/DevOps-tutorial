# Kubernetes in Docker
Prerequisite: install docker
install kind
```
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```
Install kubectl binary with curl on Linux
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
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
kubectl port-forward pod/pod-name  8989:80
kubectl port-forward svc/argocd-server  9000:80 -n argocd [local pc]
kubectl port-forward svc/argocd-server  9000:80 -n argocd --address 0.0.0.0 [cloud VM]
access from browser
localhost:8989
```
## KinD commands history
```
60  docker version

   61  vim install_docker.sh

   62  nano install_docker.sh

   63  ls

   64  sudo chmod +x install_docker.sh 

   65  ls

   66  ./install_docker.sh 

   67  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

   68  docker version

   69  sudo usermod -aG docker $USER

   70  docker version

   71  newgrp docker

   72  kind create cluster

   73  # For AMD64 / x86_64

   74  [ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-amd64

   75  # For ARM64

   76  [ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-arm64

   77  chmod +x ./kind

   78  sudo mv ./kind /usr/local/bin/kind

   79  kind version

   80  kind create cluster --name single-node-k8s

   81  docker ps

   82  kind get clusters

   83  kubectl config current-context

   84  kind versionn

   85  docker ps

   86  kind version

   87  kind get clusters

   88  kubectl config current-context

   89  kubectl apply -f https://github.com/mir-owahed/DevOps-tutorial/blob/Main/kubernetes-learn/k8s/k8s-deployment-service.yaml

   90  kubectl create deployment nginx --image nginx

   91  kubectl get pods -w

   92  kubectl get pods

   93  kubectl get svc

   94  kubectl get pods

   95  kubectl port-forward pod/nginx-5869d7778c-v8lrs  9001:8000

   96  kubectl port-forward pod/nginx-5869d7778c-v8lrs  9000:8000

   97  kubectl get all

   98  kubectl port-forward pod/nginx-5869d7778c-v8lrs  9000:80

   99  ls

  100  cd Documents/

  101  ls

  102  nano go-deploy.yaml

  103  kubectl apply -f go-deploy.yaml 

  104  kubectl get pods -w

  105  kubectl get svc

  106  kubectl port-forward svc/goapp-service 9090:8000

  107  kubectl port-forward pod/goapp-deployment-67776fc699-j5r6x 9090:8000

  108  kubectl get all

  109  kubectl delete deployment.apps/goapp-deployment

  110  kubectl delete deployment.apps/nginx 

  111  kubectl get all

  112  kubectl delete service/goapp-service

  113  kubectl delete service/kubernetes

  114  kubectl get all

  115  kind get clusters

  116  kind delete cluster

  117  kind get clusters
87  kind get clusters

   88  kind delete cluster --name single-node-k8s

   89  kind get clusters

   90  docker ps

   91  docker ps -a



  118  history

mir@ubuntu22-vm-vbox:~/Documents$ 

```
You can create a multi node cluster with the following config:

Reference:
1. <https://kind.sigs.k8s.io/>
2. <https://kind.sigs.k8s.io/docs/user/quick-start/#installation>
