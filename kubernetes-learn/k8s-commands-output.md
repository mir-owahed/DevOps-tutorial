# k8s commands input and output
```
controlplane $ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   28d   v1.29.0
node01         Ready    <none>          28d   v1.29.0
controlplane $ kubectl get nodes -o wide
NAME           STATUS   ROLES           AGE   VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
controlplane   Ready    control-plane   28d   v1.29.0   172.30.1.2    <none>        Ubuntu 20.04.5 LTS   5.4.0-131-generic   containerd://1.7.13
node01         Ready    <none>          28d   v1.29.0   172.30.2.2    <none>        Ubuntu 20.04.5 LTS   5.4.0-131-generic   containerd://1.7.13
controlplane $ ls -la
total 76
drwx------ 12 root root 4096 Apr  1 08:21 .
drwxr-xr-x 20 root root 4096 Apr  1 08:21 ..
-rw-------  1 root root  342 Apr  1 08:20 .ICEauthority
-rw-------  1 root root   57 Apr  1 08:20 .Xauthority
-rw-------  1 root root   20 Nov 13  2022 .bash_history
-rw-r--r--  1 root root 3316 Mar  3 15:16 .bashrc
drwx------  7 root root 4096 Apr  1 08:20 .cache
drwxr-xr-x  8 root root 4096 Apr  1 08:20 .config
drwx------  3 root root 4096 Apr  1 08:20 .dbus
drwx------  3 root root 4096 Apr  1 08:20 .gnupg
drwxr-xr-x  3 root root 4096 Mar  3 15:14 .kube
drwxr-xr-x  3 root root 4096 Apr  1 08:20 .local
-rw-r--r--  1 root root  161 Dec  5  2019 .profile
drwx------  2 root root 4096 Mar  3 14:24 .ssh
drwxr-xr-x  4 root root 4096 Apr  1 08:21 .theia
-rw-r--r--  1 root root  109 Mar  3 14:26 .vimrc
drwxr-xr-x  2 root root 4096 Apr  1 08:20 .vnc
-rw-r--r--  1 root root  165 Mar  3 15:13 .wget-hsts
lrwxrwxrwx  1 root root    1 Mar  3 14:26 filesystem -> /
drwx------  3 root root 4096 Mar  3 15:12 snap
controlplane $ pwd
/root
controlplane $ cd .kube/
controlplane $ ls -la
total 20
drwxr-xr-x  3 root root 4096 Mar  3 15:14 .
drwx------ 12 root root 4096 Apr  1 08:21 ..
drwxr-x---  4 root root 4096 Mar  3 15:14 cache
-rw-------  1 root root 5650 Mar  3 15:14 config
controlplane $ vim config 
controlplane $ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   28d   v1.29.0
node01         Ready    <none>          28d   v1.29.0
controlplane $ kubectl get nodes -o wide
NAME           STATUS   ROLES           AGE   VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-R
controlplane $ kubectl config current-context
kubernetes-admin@kubernetes
controlplane $ kubectl config get-clusters
NAME
kubernetes
controlplane $ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   28d   v1.29.0
node01         Ready    <none>          28d   v1.29.0
controlplane $ kubectl get namespaces
NAME                 STATUS   AGE
default              Active   28d
kube-node-lease      Active   28d
kube-public          Active   28d
kube-system          Active   28d
local-path-storage   Active   28d
controlplane $ kubectl get all       
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   28d

controlplane $ kubectl create deployment goapp --image=owahed1/k8s-hello-go:latest
deployment.apps/goapp created
controlplane $ kubectl get pods                                                   
NAME                    READY   STATUS              RESTARTS   AGE
goapp-7d5f7c6f9-rgmvf   0/1     ContainerCreating   0          9s
controlplane $ kubectl get pods -o wide
NAME                    READY   STATUS              RESTARTS   AGE   IP       NODE     NOMINATED NODE   READINESS GATES
goapp-7d5f7c6f9-rgmvf   0/1     ContainerCreating   0          18s   <none>   node01   <none>           <none>
controlplane $ kubectl get pods --watch
NAME                    READY   STATUS    RESTARTS   AGE
goapp-7d5f7c6f9-rgmvf   1/1     Running   0          38s
^Ccontrolplane $ kubectl get deployments
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
goapp   1/1     1            1           99s
controlplane $ kubectl get pods       
NAME                    READY   STATUS    RESTARTS   AGE
goapp-7d5f7c6f9-rgmvf   1/1     Running   0          109s

controlplane $ k describe pod goapp-7d5f7c6f9-rgmvf
Name:             goapp-7d5f7c6f9-rgmvf
Namespace:        default
Priority:         0
Service Account:  default
Node:             node01/172.30.2.2
Start Time:       Mon, 01 Apr 2024 08:35:35 +0000
Labels:           app=goapp
                  pod-template-hash=7d5f7c6f9
Annotations:      cni.projectcalico.org/containerID: 6b331403bef4819aac019d3949b5ad9b05216e79af5477e83dd82d72910240f8
                  cni.projectcalico.org/podIP: 192.168.1.4/32
                  cni.projectcalico.org/podIPs: 192.168.1.4/32
Status:           Running
IP:               192.168.1.4
IPs:
  IP:           192.168.1.4
Controlled By:  ReplicaSet/goapp-7d5f7c6f9
Containers:
  k8s-hello-go:
    Container ID:   containerd://3d04123c687196d89f97e23e775f8c463dd052121ba891e9b5cc47c875727527
    Image:          owahed1/k8s-hello-go:latest
    Image ID:       docker.io/owahed1/k8s-hello-go@sha256:87a50c46d964514bc5d25e19a2dd1861bee05053d5c29a0c4222f09152a118d9
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Mon, 01 Apr 2024 08:36:03 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-9fpwp (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  kube-api-access-9fpwp:
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
  Normal  Scheduled  6m4s   default-scheduler  Successfully assigned default/goapp-7d5f7c6f9-rgmvf to node01
  Normal  Pulling    6m4s   kubelet            Pulling image "owahed1/k8s-hello-go:latest"
  Normal  Pulled     5m37s  kubelet            Successfully pulled image "owahed1/k8s-hello-go:latest" in 26.638s (26.638s including waiting)
  Normal  Created    5m37s  kubelet            Created container k8s-hello-go
  Normal  Started    5m37s  kubelet            Started container k8s-hello-go
  
  controlplane $ k apply -f deployment.yaml 
deployment.apps/goapp-deployment created
controlplane $ kubectl get pod
NAME                                READY   STATUS              RESTARTS   AGE
goapp-7d5f7c6f9-rgmvf               1/1     Running             0          13m
goapp-deployment-68b465cd58-8zf42   0/1     ContainerCreating   0          8s
goapp-deployment-68b465cd58-dj5bp   1/1     Running             0          8s
goapp-deployment-68b465cd58-mtnwm   1/1     Running             0          8s
controlplane $ kubectl get pods --watch
NAME                                READY   STATUS              RESTARTS   AGE
goapp-7d5f7c6f9-rgmvf               1/1     Running             0          14m
goapp-deployment-68b465cd58-8zf42   0/1     ContainerCreating   0          18s
goapp-deployment-68b465cd58-dj5bp   1/1     Running             0          18s
goapp-deployment-68b465cd58-mtnwm   1/1     Running             0          18s
goapp-deployment-68b465cd58-8zf42   1/1     Running             0          27s
^Ccontrolplane $ kubectl get deployments      
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
goapp              1/1     1            1           15m
goapp-deployment   3/3     3            3           79s
controlplane $ k get pod
NAME                                READY   STATUS    RESTARTS   AGE
goapp-7d5f7c6f9-rgmvf               1/1     Running   0          15m
goapp-deployment-68b465cd58-8zf42   1/1     Running   0          104s
goapp-deployment-68b465cd58-dj5bp   1/1     Running   0          104s
goapp-deployment-68b465cd58-mtnwm   1/1     Running   0          104s
controlplane $ k get pod -o wide
NAME                                READY   STATUS    RESTARTS   AGE     IP            NODE           NOMINATED NODE   READINESS GATES
goapp-7d5f7c6f9-rgmvf               1/1     Running   0          16m     192.168.1.4   node01         <none>           <none>
goapp-deployment-68b465cd58-8zf42   1/1     Running   0          2m38s   192.168.0.4   controlplane   <none>           <none>
goapp-deployment-68b465cd58-dj5bp   1/1     Running   0          2m38s   192.168.1.6   node01         <none>           <none>
goapp-deployment-68b465cd58-mtnwm   1/1     Running   0          2m38s   192.168.1.5   node01         <none>           <none>

controlplane $ k describe deployments goapp-deployment
Name:                   goapp-deployment
Namespace:              default
CreationTimestamp:      Mon, 01 Apr 2024 08:49:18 +0000
Labels:                 app=goapp
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=goapp
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=goapp
  Containers:
   nginx:
    Image:        owahed1/k8s-hello-go:latest
    Port:         8000/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   goapp-deployment-68b465cd58 (3/3 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  4m41s  deployment-controller  Scaled up replica set goapp-deployment-68b465cd58 to 3
  
  controlplane $ k expose deployment/goapp-deployment --type=NodePort --port=8000
service/goapp-deployment exposed

controlplane $ k get service
NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
goapp-deployment   NodePort    10.109.206.213   <none>        8000:32591/TCP   65s
kubernetes         ClusterIP   10.96.0.1        <none>        443/TCP          28d

controlplane $ k get service
NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
goapp-deployment   NodePort    10.109.206.213   <none>        8000:32591/TCP   65s
kubernetes         ClusterIP   10.96.0.1        <none>        443/TCP          28d
controlplane $ k get nodes 
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   28d   v1.29.0
node01         Ready    <none>          28d   v1.29.0
controlplane $ ssh node01 
Last login: Sun Nov 13 17:27:09 2022 from 10.48.0.33
node01 $ curl 10.109.206.213:8000/hello
HELLO WORLD!!node01 $ curl 10.109.206.213:8000/ping
```
