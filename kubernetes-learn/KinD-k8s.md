# Kubernetes in Docker
Prerequisite: install docker

Reference 
<https://github.com/mir-owahed/DevOps-tutorial/blob/Main/docker-learn/docker-installation-sh.md>

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
KinD commands
```
kind version
kind create cluster --name single-node-k8s
kind get clusters
kubectl config current-context
kubectl config view
kubectl config use-context kind-single-node-cluster
kubectl get nodes
kubectl get sa
kubectl get sa -n kube-system
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
Run `kubectl get pods` to verify the Pods are ready and running.

Run `kubectl port-forward deployment/frontend 8080:8080` to forward a port to the frontend service.

Navigate to `localhost:8080` to access the web frontend.

You can create a multi node cluster with the following config:
```
# three node (two workers) cluster config
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker

```

## Minikube - Local Cluster 

Launch a local Kubernetes cluster with one of the following tools:

    - To launch **Minikube** (tested with Ubuntu Linux). Please, ensure that the
       local Kubernetes cluster has at least:
        - 4 CPUs
        - 4.0 GiB memory
        - 32 GB disk space

      ```shell
      minikube start --cpus=4 --memory 4096 --disk-size 32g
      ```
      ```shell
      minikube start --nodes 3 -p prod
      ```

Demo app
```
https://github.com/GoogleCloudPlatform/microservices-demo.git
```

## KinD commands history
```
mir@DESKTOP-JASRD4A:~$ kind create cluster --config kind-multi-cluster-info.yaml --name 3-node-kind-cluster
Creating cluster "3-node-kind-cluster" ...
 ✓ Ensuring node image (kindest/node:v1.32.2) 🖼
 ✓ Preparing nodes 📦 📦 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
 ✓ Joining worker nodes 🚜
Set kubectl context to "kind-3-node-kind-cluster"
You can now use your cluster with:

kubectl cluster-info --context kind-3-node-kind-cluster

Thanks for using kind! 😊
mir@DESKTOP-JASRD4A:~$ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:39995
CoreDNS is running at https://127.0.0.1:39995/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
mir@DESKTOP-JASRD4A:~$ kind get clusters
3-node-kind-cluster
mir@DESKTOP-JASRD4A:~$ kubectl config current-context
kind-3-node-kind-cluster
mir@DESKTOP-JASRD4A:~$ kind get nodes
No kind nodes found for cluster "kind".
mir@DESKTOP-JASRD4A:~$ kubectl get nodes
NAME                                STATUS   ROLES           AGE   VERSION
3-node-kind-cluster-control-plane   Ready    control-plane   18m   v1.32.2
3-node-kind-cluster-worker          Ready    <none>          18m   v1.32.2
3-node-kind-cluster-worker2         Ready    <none>          18m   v1.32.2
mir@DESKTOP-JASRD4A:~$

mir@LAPTOP-VEPS2P4F:~$ kind get clusters
single-node-cluster
mir@LAPTOP-VEPS2P4F:~$ kubectl get nodes
NAME                                STATUS   ROLES           AGE   VERSION
single-node-cluster-control-plane   Ready    control-plane   12d   v1.32.2
mir@LAPTOP-VEPS2P4F:~$ kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://127.0.0.1:43915
  name: kind-single-node-cluster
contexts:
- context:
    cluster: kind-single-node-cluster
    user: kind-single-node-cluster
  name: kind-single-node-cluster
current-context: kind-single-node-cluster
kind: Config
preferences: {}
users:
- name: kind-single-node-cluster
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED
mir@LAPTOP-VEPS2P4F:~$ kubectl config current-context
kind-single-node-cluster
mir@LAPTOP-VEPS2P4F:~$ ls
go-deploy.yaml  install_docker.sh  microservices-demo  test-vm-public_key.pem
go-lang-app     kubectl            spring-petclinic    test-vm-public_key.pem:Zone.Identifier
mir@LAPTOP-VEPS2P4F:~$

mir@LAPTOP-VEPS2P4F:~$ kubectl config current-context
kind-single-node-cluster
mir@LAPTOP-VEPS2P4F:~$ ls
go-deploy.yaml  install_docker.sh  microservices-demo  test-vm-public_key.pem
go-lang-app     kubectl            spring-petclinic    test-vm-public_key.pem:Zone.Identifier
mir@LAPTOP-VEPS2P4F:~$ vim kind-3-node-cluster-config.yaml
mir@LAPTOP-VEPS2P4F:~$ kind create cluster --config kind-3-node-cluster-config.yaml --name kind-3-node-cluster
Creating cluster "kind-3-node-cluster" ...
 ✓ Ensuring node image (kindest/node:v1.32.2) 🖼
 ✓ Preparing nodes 📦 📦 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
 ✓ Joining worker nodes 🚜
Set kubectl context to "kind-kind-3-node-cluster"
You can now use your cluster with:

kubectl cluster-info --context kind-kind-3-node-cluster

Thanks for using kind! 😊
mir@LAPTOP-VEPS2P4F:~$ kind get clusters
kind-3-node-cluster
single-node-cluster
mir@LAPTOP-VEPS2P4F:~$ kubectl config current-context
kind-kind-3-node-cluster
mir@LAPTOP-VEPS2P4F:~$ kubectl config use-context single-node-cluster
error: no context exists with the name: "single-node-cluster"
mir@LAPTOP-VEPS2P4F:~$ kubectl config use-context single-node-cluster
error: no context exists with the name: "single-node-cluster"
mir@LAPTOP-VEPS2P4F:~$ kubectl config use-context kind-single-node-cluster
Switched to context "kind-single-node-cluster".
mir@LAPTOP-VEPS2P4F:~$
mir@LAPTOP-VEPS2P4F:~$ kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://127.0.0.1:34779
  name: kind-kind-3-node-cluster
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://127.0.0.1:43915
  name: kind-single-node-cluster
contexts:
- context:
    cluster: kind-kind-3-node-cluster
    user: kind-kind-3-node-cluster
  name: kind-kind-3-node-cluster
- context:
    cluster: kind-single-node-cluster
    user: kind-single-node-cluster
  name: kind-single-node-cluster
current-context: kind-single-node-cluster
kind: Config
preferences: {}
users:
- name: kind-kind-3-node-cluster
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED
- name: kind-single-node-cluster
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED

mir@LAPTOP-VEPS2P4F:~$ kubectl config use-context kind-kind-3-node-cluster
Switched to context "kind-kind-3-node-cluster".
mir@LAPTOP-VEPS2P4F:~$ vim k8s-deployment-service.yaml
mir@LAPTOP-VEPS2P4F:~$ vim k8s-deployment-service.yaml
mir@LAPTOP-VEPS2P4F:~$ kubectl apply -f k8s-deployment-service.yaml
deployment.apps/goapp-deployment created
service/goapp-service created
mir@LAPTOP-VEPS2P4F:~$ kubectl get pods -w
NAME                                READY   STATUS              RESTARTS   AGE
goapp-deployment-67776fc699-bhrpm   0/1     ContainerCreating   0          9s
goapp-deployment-67776fc699-s9r4r   0/1     ContainerCreating   0          9s
goapp-deployment-67776fc699-bhrpm   1/1     Running             0          27s
goapp-deployment-67776fc699-s9r4r   1/1     Running             0          28s
^Cmir@LAPTOP-VEPS2P4F:~$ kubectl get all
NAME                                    READY   STATUS    RESTARTS   AGE
pod/goapp-deployment-67776fc699-bhrpm   1/1     Running   0          3m20s
pod/goapp-deployment-67776fc699-s9r4r   1/1     Running   0          3m20s

NAME                    TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
service/goapp-service   LoadBalancer   10.96.50.29   <pending>     80:31930/TCP   3m20s
service/kubernetes      ClusterIP      10.96.0.1     <none>        443/TCP        33m

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/goapp-deployment   2/2     2            2           3m20s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/goapp-deployment-67776fc699   2         2         2       3m20s
mir@LAPTOP-VEPS2P4F:~$ kubectl get deployments
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
goapp-deployment   2/2     2            2           4m16s
mir@LAPTOP-VEPS2P4F:~$ kubectl get svc
NAME            TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
goapp-service   LoadBalancer   10.96.50.29   <pending>     80:31930/TCP   4m49s
kubernetes      ClusterIP      10.96.0.1     <none>        443/TCP        34m
mir@LAPTOP-VEPS2P4F:~$ kubectl get nodes
NAME                                STATUS   ROLES           AGE   VERSION
kind-3-node-cluster-control-plane   Ready    control-plane   36m   v1.32.2
kind-3-node-cluster-worker          Ready    <none>          36m   v1.32.2
kind-3-node-cluster-worker2         Ready    <none>          36m   v1.32.2
mir@LAPTOP-VEPS2P4F:~$ kubectl port-forward service/goapp-service 8383:8000
error: Service goapp-service does not have a service port 8000
mir@LAPTOP-VEPS2P4F:~$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
goapp-deployment-67776fc699-bhrpm   1/1     Running   0          11m
goapp-deployment-67776fc699-s9r4r   1/1     Running   0          11m
mir@LAPTOP-VEPS2P4F:~$ kubectl port-forward goapp-deployment-67776fc699-bhrpm 8383:8000
Forwarding from 127.0.0.1:8383 -> 8000
Forwarding from [::1]:8383 -> 8000
Handling connection for 8383
^Cmir@LAPTOP-VEPS2P4F:~$


```


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
```
 144  docker ps
  145  vim install_docker.sh
  146  ls
  147  sudo chmod +x install_docker.sh
  148  ls
  149  ./install_docker.sh
  150  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  151  ls
  152  docker version
  153  sudo usermod -aG $USER
  154  sudo usermod -aG docker $USER
  155  docker version
  156  docker ps
  157  pwd
  158  # For AMD64 / x86_64
  159  [ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-amd64
  160  # For ARM64
  161  [ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-arm64
  162  chmod +x ./kind
  163  sudo mv ./kind /usr/local/bin/kind
  164  ls
  165  kind version
  166  kind create cluster 1-node-k8s
  167  kind create cluster --name 1-node-k8s
  168  kind get cluster
  169  kind get clusters
  170  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  171  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
  172  kubectl version --client
  173  kubectl config current-context
  174  mkdir k8s
  175  cd k8s/
  176  code .
  177  docker ps
  178  kubectl gets pods
  179  kubectl get pods
  180  nano multinode-cluster.yaml
  181  kind create cluster --name 9-node-k8s --config=multinode-cluster.yaml
  182  kubectl config current-context
  183  kubectl get clusters
  184  kubectl get cluster
  185  kind get clusters
  186  kind delete cluster
  187  kind get clusters
   189  kind delete cluster --name 1-node-k8s
  190  kind delete cluster --name 9-node-k8s
  191  history
mir@DESKTOP-JASRD4A:~/k8s$
```
You can create a multi node cluster with the following config:
```
kind create cluster --config kind-3-node-cluster-config.yaml --name kind-3-node-cluster
```
vim kind-3-node-cluster-config.yaml
```
# three node (two workers) cluster config
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

Reference:
1. <https://kind.sigs.k8s.io/>
2. <https://kind.sigs.k8s.io/docs/user/quick-start/#installation>
