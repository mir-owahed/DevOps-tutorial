# Kubectl basic commands
```
@mir-owahed ➜ ~/microservices-demo (main) $ minikube status
minikube
type: Control Plane
host: Stopped
kubelet: Stopped
apiserver: Stopped
kubeconfig: Stopped

@mir-owahed ➜ ~/microservices-demo (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ ~/microservices-demo (main) $ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED       SIZE
gcr.io/k8s-minikube/kicbase   v0.0.46   e72c4cbe9b29   3 weeks ago   1.31GB
@mir-owahed ➜ ~/microservices-demo (main) $ minikube start --nodes 3 -p test
😄  [test] minikube v1.35.0 on Ubuntu 20.04 (docker/amd64)
✨  Automatically selected the docker driver. Other choices: none, ssh
📌  Using Docker driver with root privileges
👍  Starting "test" primary control-plane node in "test" cluster
🚜  Pulling base image v0.0.46 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: default-storageclass, storage-provisioner

👍  Starting "test-m02" worker node in "test" cluster
🚜  Pulling base image v0.0.46 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🌐  Found network options:
    ▪ NO_PROXY=192.168.67.2
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ env NO_PROXY=192.168.67.2
🔎  Verifying Kubernetes components...

👍  Starting "test-m03" worker node in "test" cluster
🚜  Pulling base image v0.0.46 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🌐  Found network options:
    ▪ NO_PROXY=192.168.67.2,192.168.67.3
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ env NO_PROXY=192.168.67.2
    ▪ env NO_PROXY=192.168.67.2,192.168.67.3
🔎  Verifying Kubernetes components...
🏄  Done! kubectl is now configured to use "test" cluster and "default" namespace by default
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl config current-context 
test
@mir-owahed ➜ ~/microservices-demo (main) $ minikube status
minikube
type: Control Plane
host: Stopped
kubelet: Stopped
apiserver: Stopped
kubeconfig: Stopped

@mir-owahed ➜ ~/microservices-demo (main) $ kubectl cluster-info 
Kubernetes control plane is running at https://192.168.67.2:8443
CoreDNS is running at https://192.168.67.2:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
@mir-owahed ➜ ~/microservices-demo (main) $ kuve get nodes
bash: kuve: command not found
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl get nodes 
NAME       STATUS   ROLES           AGE     VERSION
test       Ready    control-plane   3m56s   v1.32.0
test-m02   Ready    <none>          3m15s   v1.32.0
test-m03   Ready    <none>          2m41s   v1.32.0
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl config get-c
get-clusters  (Display clusters defined in the kubeconfig)  get-contexts  (Describe one or many contexts)               
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl config get-clusters 
NAME
minikube
prod
test
@mir-owahed ➜ ~/microservices-demo (main) $ minikube stop test
✋  Stopping node "minikube"  ...
🛑  1 node stopped.
@mir-owahed ➜ ~/microservices-demo (main) $ minikube stop prod
✋  Stopping node "minikube"  ...
🛑  1 node stopped.
@mir-owahed ➜ ~/microservices-demo (main) $ minikube status
minikube
type: Control Plane
host: Stopped
kubelet: Stopped
apiserver: Stopped
kubeconfig: Stopped

@mir-owahed ➜ ~/microservices-demo (main) $ minikube start --nodes 3
😄  minikube v1.35.0 on Ubuntu 20.04 (docker/amd64)
✨  Using the docker driver based on existing profile
❗  You cannot change the number of nodes for an existing minikube cluster. Please use 'minikube node add' to add nodes to an existing cluster.
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.46 ...
🔄  Restarting existing docker container for "minikube" ...
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
    ▪ Using image docker.io/kubernetesui/metrics-scraper:v1.0.8
    ▪ Using image docker.io/kubernetesui/dashboard:v2.7.0
💡  Some dashboard features require the metrics-server addon. To enable all features please run:

        minikube addons enable metrics-server

🌟  Enabled addons: storage-provisioner, default-storageclass, dashboard
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
@mir-owahed ➜ ~/microservices-demo (main) $ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

@mir-owahed ➜ ~/microservices-demo (main) $ cd ~/.kube/
@mir-owahed ➜ ~/.kube $ ls
cache  config
@mir-owahed ➜ ~/.kube $ vi
vi          vidir       view        vigr        vim         vim.basic   vim.tiny    vimdiff     vimtutor    vipe        vipw        virtualenv  visudo      
@mir-owahed ➜ ~/.kube $ vi
vi          vidir       view        vigr        vim         vim.basic   vim.tiny    vimdiff     vimtutor    vipe        vipw        virtualenv  visudo      
@mir-owahed ➜ ~/.kube $ vim config 
@mir-owahed ➜ ~/.kube $ kubectl config get-clusters 
NAME
prod
test
minikube
@mir-owahed ➜ ~/.kube $ docker ps
CONTAINER ID   IMAGE                                 COMMAND                  CREATED          STATUS          PORTS                                                                                                                                  NAMES
ef47db1ede65   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   14 minutes ago   Up 14 minutes   127.0.0.1:32778->22/tcp, 127.0.0.1:32779->2376/tcp, 127.0.0.1:32780->5000/tcp, 127.0.0.1:32781->8443/tcp, 127.0.0.1:32782->32443/tcp   test-m03
c28b539022ce   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   14 minutes ago   Up 14 minutes   127.0.0.1:32773->22/tcp, 127.0.0.1:32774->2376/tcp, 127.0.0.1:32775->5000/tcp, 127.0.0.1:32776->8443/tcp, 127.0.0.1:32777->32443/tcp   test-m02
88ffb34087e0   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   15 minutes ago   Up 15 minutes   127.0.0.1:32768->22/tcp, 127.0.0.1:32769->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32771->8443/tcp, 127.0.0.1:32772->32443/tcp   test
15848f652909   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   2 weeks ago      Up 6 minutes    127.0.0.1:32783->22/tcp, 127.0.0.1:32784->2376/tcp, 127.0.0.1:32785->5000/tcp, 127.0.0.1:32786->8443/tcp, 127.0.0.1:32787->32443/tcp   minikube
@mir-owahed ➜ ~/.kube $ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED       SIZE
gcr.io/k8s-minikube/kicbase   v0.0.46   e72c4cbe9b29   3 weeks ago   1.31GB
@mir-owahed ➜ ~/.kube $ kubectl config current-context 
minikube
@mir-owahed ➜ ~/.kube $ cd ../microservices-demo/
@mir-owahed ➜ ~/microservices-demo (main) $ history
```
