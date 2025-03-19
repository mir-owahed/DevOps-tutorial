KinD Hands-on
```
mir@DESKTOP-JASRD4A:~$ kind get clusters
kind
mir@DESKTOP-JASRD4A:~$ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:34677
CoreDNS is running at https://127.0.0.1:34677/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
mir@DESKTOP-JASRD4A:~$ kubectl get nodes
NAME                 STATUS   ROLES           AGE   VERSION
kind-control-plane   Ready    control-plane   14m   v1.32.2
mir@DESKTOP-JASRD4A:~$ kubectl get all
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   15m
mir@DESKTOP-JASRD4A:~$ kubectl get namespace
NAME                 STATUS   AGE
default              Active   16m
kube-node-lease      Active   16m
kube-public          Active   16m
kube-system          Active   16m
local-path-storage   Active   16m
```
