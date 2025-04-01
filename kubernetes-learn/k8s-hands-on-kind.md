# Kind Hands-on
```
mir@LAPTOP-VEPS2P4F:~$ kind create cluster
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.32.2) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
mir@LAPTOP-VEPS2P4F:~$ kind get clusters
kind
mir@LAPTOP-VEPS2P4F:~$ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:33245
CoreDNS is running at https://127.0.0.1:33245/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
mir@LAPTOP-VEPS2P4F:~$ kubectl get clusters
error: the server doesn't have a resource type "clusters"
mir@LAPTOP-VEPS2P4F:~$ kubectl get cluster
error: the server doesn't have a resource type "cluster"
mir@LAPTOP-VEPS2P4F:~$ kubectl get nodes
NAME                 STATUS   ROLES           AGE     VERSION
kind-control-plane   Ready    control-plane   2m31s   v1.32.2
mir@LAPTOP-VEPS2P4F:~$
mir@LAPTOP-VEPS2P4F:~$ docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                       NAMES
e2b1e6450d77   kindest/node:v1.32.2   "/usr/local/bin/entr…"   2 minutes ago   Up 2 minutes   127.0.0.1:33245->6443/tcp   kind-control-plane
mir@LAPTOP-VEPS2P4F:~$ docker ps -a
CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                       NAMES
e2b1e6450d77   kindest/node:v1.32.2   "/usr/local/bin/entr…"   2 minutes ago   Up 2 minutes   127.0.0.1:33245->6443/tcp   kind-control-plane
mir@LAPTOP-VEPS2P4F:~$ docker images
REPOSITORY     TAG       IMAGE ID       CREATED       SIZE
kindest/node   <none>    f3e3747ca921   6 weeks ago   1.04GB
mir@LAPTOP-VEPS2P4F:~$ ls
k8s-deployment-service.yaml  kubectl  multi-node-k8s-cluster.yaml
mir@LAPTOP-VEPS2P4F:~$ kubectl get all
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   3m50s
mir@LAPTOP-VEPS2P4F:~$ kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://127.0.0.1:33245
  name: kind-kind
contexts:
- context:
    cluster: kind-kind
    user: kind-kind
  name: kind-kind
current-context: kind-kind
kind: Config
preferences: {}
users:
- name: kind-kind
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED
mir@LAPTOP-VEPS2P4F:~$ ls -la
total 56036
drwxr-x--- 6 mir  mir        4096 Apr  1 03:29 .
drwxr-xr-x 3 root root       4096 Mar 29 17:16 ..
-rw------- 1 mir  mir        2257 Mar 29 18:31 .bash_history
-rw-r--r-- 1 mir  mir         220 Mar 29 17:16 .bash_logout
-rw-r--r-- 1 mir  mir        3771 Mar 29 17:16 .bashrc
drwx------ 2 mir  mir        4096 Mar 29 17:16 .cache
drwxr-xr-x 3 mir  docker     4096 Apr  1 04:09 .kube
drwxr-xr-x 2 mir  mir        4096 Apr  1 03:29 .landscape
drwxr-xr-x 3 mir  docker     4096 Mar 29 18:06 .local
-rw-r--r-- 1 mir  mir           0 Apr  1 03:29 .motd_shown
-rw-r--r-- 1 mir  mir         807 Mar 29 17:16 .profile
-rw-r--r-- 1 mir  mir           0 Mar 29 17:44 .sudo_as_admin_successful
-rw------- 1 mir  docker     1474 Mar 29 18:16 .viminfo
-rw-r--r-- 1 mir  docker      925 Mar 29 18:16 k8s-deployment-service.yaml
-rw-r--r-- 1 mir  docker 57323672 Mar 29 18:00 kubectl
-rw-r--r-- 1 mir  docker      151 Mar 29 18:05 multi-node-k8s-cluster.yaml
mir@LAPTOP-VEPS2P4F:~$ cd .kube/
mir@LAPTOP-VEPS2P4F:~/.kube$ ls
cache  config
mir@LAPTOP-VEPS2P4F:~/.kube$ vim config
mir@LAPTOP-VEPS2P4F:~/.kube$ cd
mir@LAPTOP-VEPS2P4F:~$ kubectl config current-context
kind-kind
mir@LAPTOP-VEPS2P4F:~$ ls
k8s-deployment-service.yaml  kubectl  multi-node-k8s-cluster.yaml
mir@LAPTOP-VEPS2P4F:~$ kubectl apply -f k8s-deployment-service.yaml
deployment.apps/goapp-deployment created
service/goapp-service created
mir@LAPTOP-VEPS2P4F:~$ kueget pods -w
kueget: command not found
mir@LAPTOP-VEPS2P4F:~$ kubectl get pods -w
NAME                                READY   STATUS              RESTARTS   AGE
goapp-deployment-67776fc699-rhh47   0/1     ContainerCreating   0          18s
goapp-deployment-67776fc699-wr7fv   0/1     ContainerCreating   0          18s
goapp-deployment-67776fc699-wr7fv   1/1     Running             0          23s
goapp-deployment-67776fc699-rhh47   1/1     Running             0          25s
^Cmir@LAPTOP-VEPS2P4F:~$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
goapp-deployment-67776fc699-rhh47   1/1     Running   0          52s
goapp-deployment-67776fc699-wr7fv   1/1     Running   0          52s
mir@LAPTOP-VEPS2P4F:~$ kubectl get all
NAME                                    READY   STATUS    RESTARTS   AGE
pod/goapp-deployment-67776fc699-rhh47   1/1     Running   0          61s
pod/goapp-deployment-67776fc699-wr7fv   1/1     Running   0          61s

NAME                    TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/goapp-service   LoadBalancer   10.96.66.101   <pending>     80:30131/TCP   61s
service/kubernetes      ClusterIP      10.96.0.1      <none>        443/TCP        13m

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/goapp-deployment   2/2     2            2           61s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/goapp-deployment-67776fc699   2         2         2       61s
mir@LAPTOP-VEPS2P4F:~$ kubectl edit deployment goapp-deployment
deployment.apps/goapp-deployment edited
mir@LAPTOP-VEPS2P4F:~$ kubectl get pods -w
NAME                                READY   STATUS              RESTARTS   AGE
goapp-deployment-67776fc699-lmsns   1/1     Running             0          9s
goapp-deployment-67776fc699-rhh47   1/1     Running             0          8m35s
goapp-deployment-67776fc699-s9bnr   0/1     ContainerCreating   0          9s
goapp-deployment-67776fc699-tsv8c   1/1     Running             0          9s
goapp-deployment-67776fc699-wr7fv   1/1     Running             0          8m35s
goapp-deployment-67776fc699-s9bnr   1/1     Running             0          9s
^Cmir@LAPTOP-VEPS2P4F:~$  kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
goapp-deployment-67776fc699-lmsns   1/1     Running   0          75s
goapp-deployment-67776fc699-rhh47   1/1     Running   0          9m41s
goapp-deployment-67776fc699-s9bnr   1/1     Running   0          75s
goapp-deployment-67776fc699-tsv8c   1/1     Running   0          75s
goapp-deployment-67776fc699-wr7fv   1/1     Running   0          9m41s
mir@LAPTOP-VEPS2P4F:~$ kubectl describe pods goapp-deployment-67776fc699-lmsns
Name:             goapp-deployment-67776fc699-lmsns
Namespace:        default
Priority:         0
Service Account:  default
Node:             kind-control-plane/172.18.0.2
Start Time:       Tue, 01 Apr 2025 04:30:34 +0000
Labels:           app=goapp
                  pod-template-hash=67776fc699
Annotations:      <none>
Status:           Running
IP:               10.244.0.8
IPs:
  IP:           10.244.0.8
Controlled By:  ReplicaSet/goapp-deployment-67776fc699
Containers:
  goapp:
    Container ID:   containerd://5c731860e6926a5c9753389fa39b712db266641379619a13b7b50a432c0b78d5
    Image:          owahed1/go-lang-app:0.0.2
    Image ID:       docker.io/owahed1/go-lang-app@sha256:60fd8bf7c535868a780235fda331c4eb576de7dff03d875a3b86773b27ac09ee
    Port:           8000/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 01 Apr 2025 04:30:39 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-68vlc (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-68vlc:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m24s  default-scheduler  Successfully assigned default/goapp-deployment-67776fc699-lmsns to kind-control-plane
  Normal  Pulling    2m24s  kubelet            Pulling image "owahed1/go-lang-app:0.0.2"
  Normal  Pulled     2m20s  kubelet            Successfully pulled image "owahed1/go-lang-app:0.0.2" in 4.118s (4.118s including waiting). Image size: 93027944 bytes.
  Normal  Created    2m20s  kubelet            Created container: goapp
  Normal  Started    2m19s  kubelet            Started container goapp
mir@LAPTOP-VEPS2P4F:~$ kubectl describe pods goapp-deployment-67776fc699-lmsns | vim -
Vim: Reading from stdin...

mir@LAPTOP-VEPS2P4F:~$ kubectl describe deployment goapp-deployment | vim -
Vim: Reading from stdin...

mir@LAPTOP-VEPS2P4F:~$
mir@LAPTOP-VEPS2P4F:~$ kubectl get all
NAME                                    READY   STATUS    RESTARTS   AGE
pod/goapp-deployment-67776fc699-lmsns   1/1     Running   0          13m
pod/goapp-deployment-67776fc699-rhh47   1/1     Running   0          21m
pod/goapp-deployment-67776fc699-s9bnr   1/1     Running   0          13m
pod/goapp-deployment-67776fc699-tsv8c   1/1     Running   0          13m
pod/goapp-deployment-67776fc699-wr7fv   1/1     Running   0          21m

NAME                    TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/goapp-service   LoadBalancer   10.96.66.101   <pending>     80:30131/TCP   21m
service/kubernetes      ClusterIP      10.96.0.1      <none>        443/TCP        34m

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/goapp-deployment   5/5     5            5           21m

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/goapp-deployment-67776fc699   5         5         5       21m
mir@LAPTOP-VEPS2P4F:~$ kubectl describe service goapp-service
Name:                     goapp-service
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=goapp
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.96.66.101
IPs:                      10.96.66.101
Port:                     <unset>  80/TCP
TargetPort:               8000/TCP
NodePort:                 <unset>  30131/TCP
Endpoints:                10.244.0.6:8000,10.244.0.5:8000,10.244.0.8:8000 + 2 more...
Session Affinity:         None
External Traffic Policy:  Cluster
Internal Traffic Policy:  Cluster
Events:                   <none>
mir@LAPTOP-VEPS2P4F:~$ kind get clusters
kind
mir@LAPTOP-VEPS2P4F:~$ ls
k8s-deployment-service.yaml  kubectl  multi-node-k8s-cluster.yaml
mir@LAPTOP-VEPS2P4F:~$ kind create cluster --name=3-node-cluster --config=multi-node-k8s-cluster.yaml
Creating cluster "3-node-cluster" ...
 ✓ Ensuring node image (kindest/node:v1.32.2) 🖼
 ✓ Preparing nodes 📦 📦 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
 ✓ Joining worker nodes 🚜
Set kubectl context to "kind-3-node-cluster"
You can now use your cluster with:

kubectl cluster-info --context kind-3-node-cluster

Thanks for using kind! 😊
mir@LAPTOP-VEPS2P4F:~$ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:40347
CoreDNS is running at https://127.0.0.1:40347/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
mir@LAPTOP-VEPS2P4F:~$ kind get clusters
3-node-cluster
kind
mir@LAPTOP-VEPS2P4F:~$ kubectl get nodes
NAME                           STATUS   ROLES           AGE     VERSION
3-node-cluster-control-plane   Ready    control-plane   7m3s    v1.32.2
3-node-cluster-worker          Ready    <none>          6m52s   v1.32.2
3-node-cluster-worker2         Ready    <none>          6m52s   v1.32.2
mir@LAPTOP-VEPS2P4F:~$ kubectl config current-context
kind-3-node-cluster
mir@LAPTOP-VEPS2P4F:~$ kubectl get all
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   10m
mir@LAPTOP-VEPS2P4F:~$ kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://127.0.0.1:40347
  name: kind-3-node-cluster
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://127.0.0.1:33245
  name: kind-kind
contexts:
- context:
    cluster: kind-3-node-cluster
    user: kind-3-node-cluster
  name: kind-3-node-cluster
- context:
    cluster: kind-kind
    user: kind-kind
  name: kind-kind
current-context: kind-3-node-cluster
kind: Config
preferences: {}
users:
- name: kind-3-node-cluster
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED
- name: kind-kind
  user:
    client-certificate-data: DATA+OMITTED
    client-key-data: DATA+OMITTED
mir@LAPTOP-VEPS2P4F:~$ kubectl config use-context kind-kind
Switched to context "kind-kind".
mir@LAPTOP-VEPS2P4F:~$ kubectl config use-context kind-3-node-cluster
Switched to context "kind-3-node-cluster".
mir@LAPTOP-VEPS2P4F:~$ ls -la
total 56044
drwxr-x--- 6 mir  mir        4096 Apr  1 04:43 .
drwxr-xr-x 3 root root       4096 Mar 29 17:16 ..
-rw------- 1 mir  mir        2257 Mar 29 18:31 .bash_history
-rw-r--r-- 1 mir  mir         220 Mar 29 17:16 .bash_logout
-rw-r--r-- 1 mir  mir        3771 Mar 29 17:16 .bashrc
drwx------ 2 mir  mir        4096 Mar 29 17:16 .cache
drwxr-xr-x 3 mir  docker     4096 Apr  1 05:17 .kube
drwxr-xr-x 2 mir  mir        4096 Apr  1 03:29 .landscape
drwxr-xr-x 3 mir  docker     4096 Mar 29 18:06 .local
-rw-r--r-- 1 mir  mir           0 Apr  1 03:29 .motd_shown
-rw-r--r-- 1 mir  mir         807 Mar 29 17:16 .profile
-rw-r--r-- 1 mir  mir           0 Mar 29 17:44 .sudo_as_admin_successful
-rw------- 1 mir  docker    10119 Apr  1 04:43 .viminfo
-rw-r--r-- 1 mir  docker      925 Mar 29 18:16 k8s-deployment-service.yaml
-rw-r--r-- 1 mir  docker 57323672 Mar 29 18:00 kubectl
-rw-r--r-- 1 mir  docker      151 Mar 29 18:05 multi-node-k8s-cluster.yaml
mir@LAPTOP-VEPS2P4F:~$ cd .kube/
mir@LAPTOP-VEPS2P4F:~/.kube$ vim config
mir@LAPTOP-VEPS2P4F:~/.kube$ cd
mir@LAPTOP-VEPS2P4F:~$ ls
k8s-deployment-service.yaml  kubectl  multi-node-k8s-cluster.yaml
mir@LAPTOP-VEPS2P4F:~$ kubectl apply -f multi-node-k8s-cluster.yaml
error: resource mapping not found for name: "" namespace: "" from "multi-node-k8s-cluster.yaml": no matches for kind "Cluster" in version "kind.x-k8s.io/v1alpha4"
ensure CRDs are installed first
mir@LAPTOP-VEPS2P4F:~$ ls
k8s-deployment-service.yaml  kubectl  multi-node-k8s-cluster.yaml
mir@LAPTOP-VEPS2P4F:~$ kubectl apply -f k8s-deployment-service.yaml
deployment.apps/goapp-deployment created
service/goapp-service created
mir@LAPTOP-VEPS2P4F:~$ kubectl get pods -w
```
