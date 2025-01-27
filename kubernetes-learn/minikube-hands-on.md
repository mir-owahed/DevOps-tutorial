# Minikube hands-on at Codespaces
```
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED       SIZE
gcr.io/k8s-minikube/kicbase   v0.0.46   e72c4cbe9b29   13 days ago   1.31GB
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ minikube start --nodes 3 -p prod
😄  [prod] minikube v1.35.0 on Ubuntu 20.04 (docker/amd64)
✨  Using the docker driver based on existing profile
❗  You cannot change the number of nodes for an existing minikube cluster. Please use 'minikube node add' to add nodes to an existing cluster.
👍  Starting "prod" primary control-plane node in "prod" cluster
🚜  Pulling base image v0.0.46 ...
🔄  Restarting existing docker container for "prod" ...
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
🔎  Verifying Kubernetes components...
🌟  Enabled addons: 

👍  Starting "prod-m02" worker node in "prod" cluster
🚜  Pulling base image v0.0.46 ...
🔄  Restarting existing docker container for "prod-m02" ...
🌐  Found network options:
    ▪ NO_PROXY=192.168.58.2
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ env NO_PROXY=192.168.58.2
🔎  Verifying Kubernetes components...

👍  Starting "prod-m03" worker node in "prod" cluster
🚜  Pulling base image v0.0.46 ...
🔄  Restarting existing docker container for "prod-m03" ...
🌐  Found network options:
    ▪ NO_PROXY=192.168.58.2,192.168.58.3
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ env NO_PROXY=192.168.58.2
    ▪ env NO_PROXY=192.168.58.2,192.168.58.3
🔎  Verifying Kubernetes components...
🏄  Done! kubectl is now configured to use "prod" cluster and "default" namespace by default
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ minikube status -p prod
prod
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

prod-m02
type: Worker
host: Running
kubelet: Running

prod-m03
type: Worker
host: Running
kubelet: Running

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE                                 COMMAND                  CREATED          STATUS         PORTS                                                                                                                                  NAMES
a8643532d4c7   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   13 minutes ago   Up 4 minutes   127.0.0.1:32778->22/tcp, 127.0.0.1:32779->2376/tcp, 127.0.0.1:32780->5000/tcp, 127.0.0.1:32781->8443/tcp, 127.0.0.1:32782->32443/tcp   prod-m03
521fc1be712c   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   14 minutes ago   Up 4 minutes   127.0.0.1:32773->22/tcp, 127.0.0.1:32774->2376/tcp, 127.0.0.1:32775->5000/tcp, 127.0.0.1:32776->8443/tcp, 127.0.0.1:32777->32443/tcp   prod-m02
6d10470a5213   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   14 minutes ago   Up 5 minutes   127.0.0.1:32768->22/tcp, 127.0.0.1:32769->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32771->8443/tcp, 127.0.0.1:32772->32443/tcp   prod

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE                                 COMMAND                  CREATED          STATUS          PORTS                                                                                                                                  NAMES
a8643532d4c7   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   30 minutes ago   Up 21 minutes   127.0.0.1:32778->22/tcp, 127.0.0.1:32779->2376/tcp, 127.0.0.1:32780->5000/tcp, 127.0.0.1:32781->8443/tcp, 127.0.0.1:32782->32443/tcp   prod-m03
521fc1be712c   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   31 minutes ago   Up 22 minutes   127.0.0.1:32773->22/tcp, 127.0.0.1:32774->2376/tcp, 127.0.0.1:32775->5000/tcp, 127.0.0.1:32776->8443/tcp, 127.0.0.1:32777->32443/tcp   prod-m02
6d10470a5213   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   32 minutes ago   Up 22 minutes   127.0.0.1:32768->22/tcp, 127.0.0.1:32769->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32771->8443/tcp, 127.0.0.1:32772->32443/tcp   prod
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker exec -it 521fc1be712c /bin/bash
root@prod-m02:/# docker ps
CONTAINER ID   IMAGE                        COMMAND                  CREATED          STATUS          PORTS     NAMES
f983359c596e   50415e5d05f0                 "/bin/kindnetd"          24 minutes ago   Up 23 minutes             k8s_kindnet-cni_kindnet-jj24b_kube-system_15a36ae6-f616-4c89-80e5-a425f43306ac_1
3c225b926a6f   040f9f8aac8c                 "/usr/local/bin/kube…"   24 minutes ago   Up 23 minutes             k8s_kube-proxy_kube-proxy-vnngk_kube-system_dc439012-3f29-4955-9e8d-0f0a81436ae9_1
68a70a89e650   registry.k8s.io/pause:3.10   "/pause"                 24 minutes ago   Up 23 minutes             k8s_POD_kindnet-jj24b_kube-system_15a36ae6-f616-4c89-80e5-a425f43306ac_1
029e2f8e88a4   registry.k8s.io/pause:3.10   "/pause"                 24 minutes ago   Up 23 minutes             k8s_POD_kube-proxy-vnngk_kube-system_dc439012-3f29-4955-9e8d-0f0a81436ae9_1
root@prod-m02:/#
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker exec -it 6d10470a5213 /bin/bash
root@prod:/# docker ps
CONTAINER ID   IMAGE                        COMMAND                  CREATED          STATUS          PORTS     NAMES
eb0cdf9a5c74   6e38f40d628d                 "/storage-provisioner"   27 minutes ago   Up 27 minutes             k8s_storage-provisioner_storage-provisioner_kube-system_3940ac58-3c94-4a35-8869-28d8a79a0edb_3
61ed7289380d   c69fa2e9cbf5                 "/coredns -conf /etc…"   27 minutes ago   Up 27 minutes             k8s_coredns_coredns-668d6bf9bc-9npq7_kube-system_e50e60b2-ce55-4318-97c6-4e5593429eab_3
2bc7f16ce896   040f9f8aac8c                 "/usr/local/bin/kube…"   27 minutes ago   Up 27 minutes             k8s_kube-proxy_kube-proxy-kxz9k_kube-system_f7c8e42f-65e4-48db-a089-95f9bb5bef13_1
a948ac9ab168   50415e5d05f0                 "/bin/kindnetd"          27 minutes ago   Up 27 minutes             k8s_kindnet-cni_kindnet-lbf6m_kube-system_e75cf7c0-c7a9-43b0-b77b-c00198f518a6_1
3a2c1a673217   registry.k8s.io/pause:3.10   "/pause"                 27 minutes ago   Up 27 minutes             k8s_POD_coredns-668d6bf9bc-9npq7_kube-system_e50e60b2-ce55-4318-97c6-4e5593429eab_3
eb179fe43649   registry.k8s.io/pause:3.10   "/pause"                 27 minutes ago   Up 27 minutes             k8s_POD_kindnet-lbf6m_kube-system_e75cf7c0-c7a9-43b0-b77b-c00198f518a6_1
ac78ebe5d6b4   registry.k8s.io/pause:3.10   "/pause"                 27 minutes ago   Up 27 minutes             k8s_POD_kube-proxy-kxz9k_kube-system_f7c8e42f-65e4-48db-a089-95f9bb5bef13_1
f9d0a4946c9c   registry.k8s.io/pause:3.10   "/pause"                 27 minutes ago   Up 27 minutes             k8s_POD_storage-provisioner_kube-system_3940ac58-3c94-4a35-8869-28d8a79a0edb_1
cc490120340c   a389e107f4ff                 "kube-scheduler --au…"   28 minutes ago   Up 28 minutes             k8s_kube-scheduler_kube-scheduler-prod_kube-system_c10be55b810257607439a1ae078d0e44_1
710e9a850acd   a9e7e6b294ba                 "etcd --advertise-cl…"   28 minutes ago   Up 28 minutes             k8s_etcd_etcd-prod_kube-system_32353621445469e1dbe68817685fcdcf_1
6d42fb0886ba   c2e17b8d0f4a                 "kube-apiserver --ad…"   28 minutes ago   Up 28 minutes             k8s_kube-apiserver_kube-apiserver-prod_kube-system_e8f940a1d72dce3117fda5397473a78d_1
d4cb46b28ee9   8cab3d2a8bd0                 "kube-controller-man…"   28 minutes ago   Up 28 minutes             k8s_kube-controller-manager_kube-controller-manager-prod_kube-system_89748744e274f901cde86401741cf02f_1
2ab59948c01b   registry.k8s.io/pause:3.10   "/pause"                 28 minutes ago   Up 28 minutes             k8s_POD_etcd-prod_kube-system_32353621445469e1dbe68817685fcdcf_1
90adfa0e7425   registry.k8s.io/pause:3.10   "/pause"                 28 minutes ago   Up 28 minutes             k8s_POD_kube-apiserver-prod_kube-system_e8f940a1d72dce3117fda5397473a78d_1
591979809ac3   registry.k8s.io/pause:3.10   "/pause"                 28 minutes ago   Up 28 minutes             k8s_POD_kube-scheduler-prod_kube-system_c10be55b810257607439a1ae078d0e44_1
82128155b775   registry.k8s.io/pause:3.10   "/pause"                 28 minutes ago   Up 28 minutes             k8s_POD_kube-controller-manager-prod_kube-system_89748744e274f901cde86401741cf02f_1
root@prod:/#


