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
@mir-owahed ➜ ~/microservices-demo (main) $ ls
LICENSE  README.md  cloudbuild.yaml  docs  helm-chart  istio-manifests  kubernetes-manifests  kustomize  protos  release  skaffold.yaml  src  terraform
@mir-owahed ➜ ~/microservices-demo (main) $ ls -la
total 104
drwxr-sr-x 14 codespace codespace  4096 Feb  7 04:40 .
drwxrwsr-x  1 codespace codespace  4096 Feb  7 05:02 ..
drwxr-sr-x  4 codespace codespace  4096 Feb  7 04:40 .deploystack
-rw-r--r--  1 codespace codespace   401 Feb  7 04:40 .editorconfig
drwxr-sr-x  8 codespace codespace  4096 Feb  7 04:41 .git
-rw-r--r--  1 codespace codespace   201 Feb  7 04:40 .gitattributes
drwxr-sr-x  6 codespace codespace  4096 Feb  7 04:40 .github
-rw-r--r--  1 codespace codespace   310 Feb  7 04:40 .gitignore
-rw-r--r--  1 codespace codespace 11358 Feb  7 04:40 LICENSE
-rw-r--r--  1 codespace codespace 11812 Feb  7 04:40 README.md
-rw-r--r--  1 codespace codespace  1490 Feb  7 04:40 cloudbuild.yaml
drwxr-sr-x  4 codespace codespace  4096 Feb  7 04:40 docs
drwxr-sr-x  3 codespace codespace  4096 Feb  7 04:40 helm-chart
drwxr-sr-x  2 codespace codespace  4096 Feb  7 04:40 istio-manifests
drwxr-sr-x  2 codespace codespace  4096 Feb  7 04:40 kubernetes-manifests
drwxr-sr-x  5 codespace codespace  4096 Feb  7 04:40 kustomize
drwxr-sr-x  3 codespace codespace  4096 Feb  7 04:40 protos
drwxr-sr-x  2 codespace codespace  4096 Feb  7 04:40 release
-rw-r--r--  1 codespace codespace  3314 Feb  7 04:40 skaffold.yaml
drwxr-sr-x 14 codespace codespace  4096 Feb  7 04:40 src
drwxr-sr-x  2 codespace codespace  4096 Feb  7 04:40 terraform

@mir-owahed ➜ ~/microservices-demo (main) $ docker build -t frontend:0.0.1 -f src/frontend/Dockerfile .
[+] Building 5.9s (15/15) FINISHED                                                                                                                             docker:default
 => [internal] load build definition from Dockerfile                                                                                                                     0.1s
 => => transferring dockerfile: 1.46kB                                                                                                                                   0.0s
 => [internal] load metadata for docker.io/library/golang:1.23.4-alpine@sha256:c23339199a08b0e12032856908589a6d41a0dab141b8b3b21f156fc571a3f1d3                          2.5s
 => [auth] library/golang:pull token for registry-1.docker.io                                                                                                            0.0s
 => [internal] load .dockerignore                                                                                                                                        0.0s
 => => transferring context: 2B                                                                                                                                          0.0s
 => CANCELED [builder 1/6] FROM docker.io/library/golang:1.23.4-alpine@sha256:c23339199a08b0e12032856908589a6d41a0dab141b8b3b21f156fc571a3f1d3                           2.8s
 => => resolve docker.io/library/golang:1.23.4-alpine@sha256:c23339199a08b0e12032856908589a6d41a0dab141b8b3b21f156fc571a3f1d3                                            0.0s
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl apply -f release/kubernetes-manifests.yaml 
deployment.apps/emailservice created
service/emailservice created
serviceaccount/emailservice created
deployment.apps/checkoutservice created
service/checkoutservice created
serviceaccount/checkoutservice created
deployment.apps/recommendationservice created
service/recommendationservice created
serviceaccount/recommendationservice created
deployment.apps/frontend created
service/frontend created
service/frontend-external created
serviceaccount/frontend created
deployment.apps/paymentservice created
service/paymentservice created
serviceaccount/paymentservice created
deployment.apps/productcatalogservice created
service/productcatalogservice created
serviceaccount/productcatalogservice created
deployment.apps/cartservice created
service/cartservice created
serviceaccount/cartservice created
deployment.apps/redis-cart created
service/redis-cart created
deployment.apps/loadgenerator created
serviceaccount/loadgenerator created
deployment.apps/currencyservice created
service/currencyservice created
serviceaccount/currencyservice created
deployment.apps/shippingservice created
service/shippingservice created
serviceaccount/shippingservice created
deployment.apps/adservice created
service/adservice created
serviceaccount/adservice created
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl get pod -o wide
NAME                                                 READY   STATUS              RESTARTS      AGE   IP             NODE       NOMINATED NODE   READINESS GATES
adservice-8568877bf9-8cl7l                           0/1     Pending             0             11s   <none>         <none>     <none>           <none>
cartservice-f84bf7dd4-rwjmp                          0/1     ContainerCreating   0             13s   <none>         minikube   <none>           <none>
checkoutservice-5d9894c787-5bths                     0/1     ContainerCreating   0             13s   <none>         minikube   <none>           <none>
currencyservice-84459c6759-6xv6p                     0/1     Pending             0             12s   <none>         <none>     <none>           <none>
emailservice-6fb4dd89fc-qgfw2                        0/1     ContainerCreating   0             13s   <none>         minikube   <none>           <none>
frontend-754cdbf884-4g6cr                            0/1     ContainerCreating   0             13s   <none>         minikube   <none>           <none>
grafana-7f47bb8f55-srqwb                             1/1     Running             2 (64m ago)   9d    10.244.0.31    minikube   <none>           <none>
loadgenerator-696d89b74f-9bwmt                       0/1     Init:0/1            0             12s   <none>         minikube   <none>           <none>
paymentservice-5575668b5c-8snqg                      0/1     ContainerCreating   0             13s   <none>         minikube   <none>           <none>
productcatalogservice-59cf6fd7b5-mtdgt               0/1     ContainerCreating   0             13s   <none>         minikube   <none>           <none>
prometheus-alertmanager-0                            1/1     Running             2 (64m ago)   9d    10.244.0.37    minikube   <none>           <none>
prometheus-kube-state-metrics-5cb7f5d847-8scpc       1/1     Running             2 (64m ago)   9d    10.244.0.38    minikube   <none>           <none>
prometheus-prometheus-node-exporter-ftw5m            1/1     Running             2 (64m ago)   9d    192.168.49.2   minikube   <none>           <none>
prometheus-prometheus-pushgateway-76465f5849-b4kpm   1/1     Running             2 (64m ago)   9d    10.244.0.32    minikube   <none>           <none>
prometheus-server-5dbdb658f9-zhxss                   2/2     Running             4 (64m ago)   9d    10.244.0.35    minikube   <none>           <none>
recommendationservice-589895488f-xr6qb               0/1     ContainerCreating   0             13s   <none>         minikube   <none>           <none>
redis-cart-c4fc658fb-plq5v                           0/1     ContainerCreating   0             12s   <none>         minikube   <none>           <none>
shippingservice-fb4c9695c-7lrdn                      0/1     Pending             0             12s   <none>         <none>     <none>           <none>

@mir-owahed ➜ ~/microservices-demo (main) $ kubectl get pods --watch
NAME                                                 READY   STATUS              RESTARTS      AGE
adservice-8568877bf9-8cl7l                           0/1     Pending             0             104s
cartservice-f84bf7dd4-rwjmp                          0/1     Running             0             106s
checkoutservice-5d9894c787-5bths                     1/1     Running             0             106s
currencyservice-84459c6759-6xv6p                     0/1     Pending             0             105s
emailservice-6fb4dd89fc-qgfw2                        1/1     Running             0             106s
frontend-754cdbf884-4g6cr                            1/1     Running             0             106s
grafana-7f47bb8f55-srqwb                             1/1     Running             2 (65m ago)   9d
loadgenerator-696d89b74f-9bwmt                       0/1     Init:0/1            0             105s
paymentservice-5575668b5c-8snqg                      1/1     Running             0             106s
productcatalogservice-59cf6fd7b5-mtdgt               1/1     Running             0             106s
prometheus-alertmanager-0                            1/1     Running             2 (65m ago)   9d
prometheus-kube-state-metrics-5cb7f5d847-8scpc       1/1     Running             2 (65m ago)   9d
prometheus-prometheus-node-exporter-ftw5m            1/1     Running             2 (65m ago)   9d
prometheus-prometheus-pushgateway-76465f5849-b4kpm   1/1     Running             2 (65m ago)   9d
prometheus-server-5dbdb658f9-zhxss                   2/2     Running             4 (65m ago)   9d
recommendationservice-589895488f-xr6qb               0/1     ContainerCreating   0             106s
redis-cart-c4fc658fb-plq5v                           1/1     Running             0             105s
shippingservice-fb4c9695c-7lrdn                      0/1     Pending             0             105s




recommendationservice-589895488f-xr6qb               0/1     Running             0             114s
recommendationservice-589895488f-xr6qb               1/1     Running             0             2m1s
cartservice-f84bf7dd4-rwjmp                          1/1     Running             0             2m3s

loadgenerator-696d89b74f-9bwmt                       0/1     Init:Error          0             3m23s
loadgenerator-696d89b74f-9bwmt                       0/1     Init:0/1            1 (4s ago)    3m26s
loadgenerator-696d89b74f-9bwmt                       0/1     Init:Error          1 (2m5s ago)   5m27s
loadgenerator-696d89b74f-9bwmt                       0/1     Init:CrashLoopBackOff   1 (14s ago)    5m40s
loadgenerator-696d89b74f-9bwmt                       0/1     Init:0/1                2 (18s ago)    5m44s

@mir-owahed ➜ ~/microservices-demo (main) $ kubectl get all
NAME                                                     READY   STATUS                  RESTARTS      AGE
pod/adservice-8568877bf9-8cl7l                           0/1     Pending                 0             8m10s
pod/cartservice-f84bf7dd4-rwjmp                          1/1     Running                 0             8m12s
pod/checkoutservice-5d9894c787-5bths                     1/1     Running                 0             8m12s
pod/currencyservice-84459c6759-6xv6p                     0/1     Pending                 0             8m11s
pod/emailservice-6fb4dd89fc-qgfw2                        1/1     Running                 0             8m12s
pod/frontend-754cdbf884-4g6cr                            1/1     Running                 0             8m12s
pod/grafana-7f47bb8f55-srqwb                             1/1     Running                 2 (72m ago)   9d
pod/loadgenerator-696d89b74f-9bwmt                       0/1     Init:CrashLoopBackOff   2 (28s ago)   8m11s
pod/paymentservice-5575668b5c-8snqg                      1/1     Running                 0             8m12s
pod/productcatalogservice-59cf6fd7b5-mtdgt               1/1     Running                 0             8m12s
pod/prometheus-alertmanager-0                            1/1     Running                 2 (72m ago)   9d
pod/prometheus-kube-state-metrics-5cb7f5d847-8scpc       1/1     Running                 2 (72m ago)   9d
pod/prometheus-prometheus-node-exporter-ftw5m            1/1     Running                 2 (72m ago)   9d
pod/prometheus-prometheus-pushgateway-76465f5849-b4kpm   1/1     Running                 2 (72m ago)   9d
pod/prometheus-server-5dbdb658f9-zhxss                   2/2     Running                 4 (72m ago)   9d
pod/recommendationservice-589895488f-xr6qb               1/1     Running                 0             8m12s
pod/redis-cart-c4fc658fb-plq5v                           1/1     Running                 0             8m11s
pod/shippingservice-fb4c9695c-7lrdn                      0/1     Pending                 0             8m11s

NAME                                          TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
service/adservice                             ClusterIP      10.103.187.184   <none>        9555/TCP       8m11s
service/cartservice                           ClusterIP      10.102.22.238    <none>        7070/TCP       8m12s
service/checkoutservice                       ClusterIP      10.106.204.37    <none>        5050/TCP       8m13s
service/currencyservice                       ClusterIP      10.111.26.130    <none>        7000/TCP       8m11s
service/emailservice                          ClusterIP      10.103.113.234   <none>        5000/TCP       8m13s
service/frontend                              ClusterIP      10.100.43.81     <none>        80/TCP         8m12s
service/frontend-external                     LoadBalancer   10.110.42.59     <pending>     80:31938/TCP   8m12s
service/grafana                               ClusterIP      10.97.61.0       <none>        80/TCP         9d
service/grafana-ext                           NodePort       10.109.74.11     <none>        80:32689/TCP   9d
service/kubernetes                            ClusterIP      10.96.0.1        <none>        443/TCP        14d
service/paymentservice                        ClusterIP      10.96.253.27     <none>        50051/TCP      8m12s
service/productcatalogservice                 ClusterIP      10.110.44.48     <none>        3550/TCP       8m12s
service/prometheus-alertmanager               ClusterIP      10.105.104.1     <none>        9093/TCP       9d
service/prometheus-alertmanager-headless      ClusterIP      None             <none>        9093/TCP       9d
service/prometheus-kube-state-metrics         ClusterIP      10.99.190.239    <none>        8080/TCP       9d
service/prometheus-prometheus-node-exporter   ClusterIP      10.99.131.181    <none>        9100/TCP       9d
service/prometheus-prometheus-pushgateway     ClusterIP      10.111.84.177    <none>        9091/TCP       9d
service/prometheus-server                     ClusterIP      10.100.53.156    <none>        80/TCP         9d
service/prometheus-server-ext                 NodePort       10.101.118.16    <none>        80:30645/TCP   9d
service/recommendationservice                 ClusterIP      10.98.93.213     <none>        8080/TCP       8m12s
service/redis-cart                            ClusterIP      10.104.117.215   <none>        6379/TCP       8m12s
service/shippingservice                       ClusterIP      10.97.224.149    <none>        50051/TCP      8m11s

NAME                                                 DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
daemonset.apps/prometheus-prometheus-node-exporter   1         1         1       1            1           kubernetes.io/os=linux   9d

NAME                                                READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/adservice                           0/1     1            0           8m11s
deployment.apps/cartservice                         1/1     1            1           8m12s
deployment.apps/checkoutservice                     1/1     1            1           8m13s
deployment.apps/currencyservice                     0/1     1            0           8m11s
deployment.apps/emailservice                        1/1     1            1           8m13s
deployment.apps/frontend                            1/1     1            1           8m12s
deployment.apps/grafana                             1/1     1            1           9d
deployment.apps/loadgenerator                       0/1     1            0           8m12s
deployment.apps/paymentservice                      1/1     1            1           8m12s
deployment.apps/productcatalogservice               1/1     1            1           8m12s
deployment.apps/prometheus-kube-state-metrics       1/1     1            1           9d
deployment.apps/prometheus-prometheus-pushgateway   1/1     1            1           9d
deployment.apps/prometheus-server                   1/1     1            1           9d
deployment.apps/recommendationservice               1/1     1            1           8m12s
deployment.apps/redis-cart                          1/1     1            1           8m12s
deployment.apps/shippingservice                     0/1     1            0           8m11s

NAME                                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/adservice-8568877bf9                           1         1         0       8m11s
replicaset.apps/cartservice-f84bf7dd4                          1         1         1       8m12s
replicaset.apps/checkoutservice-5d9894c787                     1         1         1       8m12s
replicaset.apps/currencyservice-84459c6759                     1         1         0       8m11s
replicaset.apps/emailservice-6fb4dd89fc                        1         1         1       8m12s
replicaset.apps/frontend-754cdbf884                            1         1         1       8m12s
replicaset.apps/grafana-7f47bb8f55                             1         1         1       9d
replicaset.apps/loadgenerator-696d89b74f                       1         1         0       8m12s
replicaset.apps/paymentservice-5575668b5c                      1         1         1       8m12s
replicaset.apps/productcatalogservice-59cf6fd7b5               1         1         1       8m12s
replicaset.apps/prometheus-kube-state-metrics-5cb7f5d847       1         1         1       9d
replicaset.apps/prometheus-prometheus-pushgateway-76465f5849   1         1         1       9d
replicaset.apps/prometheus-server-5dbdb658f9                   1         1         1       9d
replicaset.apps/recommendationservice-589895488f               1         1         1       8m12s
replicaset.apps/redis-cart-c4fc658fb                           1         1         1       8m12s
replicaset.apps/shippingservice-fb4c9695c                      1         1         0       8m11s

NAME                                       READY   AGE
statefulset.apps/prometheus-alertmanager   1/1     9d
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl describe pod frontend-754cdbf884-4g6cr | vim -
Vim: Reading from stdin...

@mir-owahed ➜ ~/microservices-demo (main) $ kubectl get service
NAME                                  TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
adservice                             ClusterIP      10.103.187.184   <none>        9555/TCP       27m
cartservice                           ClusterIP      10.102.22.238    <none>        7070/TCP       27m
checkoutservice                       ClusterIP      10.106.204.37    <none>        5050/TCP       27m
currencyservice                       ClusterIP      10.111.26.130    <none>        7000/TCP       27m
emailservice                          ClusterIP      10.103.113.234   <none>        5000/TCP       27m
frontend                              ClusterIP      10.100.43.81     <none>        80/TCP         27m
frontend-external                     LoadBalancer   10.110.42.59     <pending>     80:31938/TCP   27m
grafana                               ClusterIP      10.97.61.0       <none>        80/TCP         9d
grafana-ext                           NodePort       10.109.74.11     <none>        80:32689/TCP   9d
kubernetes                            ClusterIP      10.96.0.1        <none>        443/TCP        14d
paymentservice                        ClusterIP      10.96.253.27     <none>        50051/TCP      27m
productcatalogservice                 ClusterIP      10.110.44.48     <none>        3550/TCP       27m
prometheus-alertmanager               ClusterIP      10.105.104.1     <none>        9093/TCP       9d
prometheus-alertmanager-headless      ClusterIP      None             <none>        9093/TCP       9d
prometheus-kube-state-metrics         ClusterIP      10.99.190.239    <none>        8080/TCP       9d
prometheus-prometheus-node-exporter   ClusterIP      10.99.131.181    <none>        9100/TCP       9d
prometheus-prometheus-pushgateway     ClusterIP      10.111.84.177    <none>        9091/TCP       9d
prometheus-server                     ClusterIP      10.100.53.156    <none>        80/TCP         9d
prometheus-server-ext                 NodePort       10.101.118.16    <none>        80:30645/TCP   9d
recommendationservice                 ClusterIP      10.98.93.213     <none>        8080/TCP       27m
redis-cart                            ClusterIP      10.104.117.215   <none>        6379/TCP       27m
shippingservice                       ClusterIP      10.97.224.149    <none>        50051/TCP      27m
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl logs --help
Print the logs for a container in a pod or specified resource. If the pod has only one container, the container name is
optional.

Examples:
  # Return snapshot logs from pod nginx with only one container
  kubectl logs nginx

prometheus-server
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl delete deployments.apps adservice cartservice checkoutservice
deployment.apps "adservice" deleted
deployment.apps "cartservice" deleted
deployment.apps "checkoutservice" deleted
@mir-owahed ➜ ~/microservices-demo (main) $ kubectl delete deployments.apps currencyservice emailservice frontend grafana loadgenerator paymentservice productcatalogservice
deployment.apps "currencyservice" deleted
deployment.apps "emailservice" deleted
deployment.apps "frontend" deleted
deployment.apps "grafana" deleted
deployment.apps "loadgenerator" deleted
deployment.apps "paymentservice" deleted
deployment.apps "productcatalogservice" deleted

@mir-owahed ➜ ~/microservices-demo (main) $ kubectl delete service adservice
service "adservice" deleted

@mir-owahed ➜ ~/microservices-demo (main) $ kubectl delete service adservice
service "adservice" deleted
@mir-owahed ➜ ~/microservices-demo (main) $ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

@mir-owahed ➜ ~/microservices-demo (main) $ minikube stop
✋  Stopping node "minikube"  ...
🛑  Powering off "minikube" via SSH ...
🛑  1 node stopped.


```
