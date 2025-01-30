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
```
## Minikube

```
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ minikube status
minikube
type: Control Plane
host: Stopped
kubelet: Stopped
apiserver: Stopped
kubeconfig: Stopped

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ minikube start
😄  minikube v1.35.0 on Ubuntu 20.04 (docker/amd64)
✨  Using the docker driver based on existing profile
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
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get all
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   4d4h
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ 
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm version 
version.BuildInfo{Version:"v3.16.3", GitCommit:"cfd07493f46efc9debd9cc1b02a0961186df7fdf", GitTreeState:"clean", GoVersion:"go1.22.7"}
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm repo ls
NAME    URL                               
bitnami https://charts.bitnami.com/bitnami
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
"prometheus-community" has been added to your repositories
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "prometheus-community" chart repository
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈Happy Helming!⎈
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm install prometheus prometheus-community/prometheus
NAME: prometheus
LAST DEPLOYED: Tue Jan 28 09:51:45 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
The Prometheus server can be accessed via port 80 on the following DNS name from within your cluster:
prometheus-server.default.svc.cluster.local


Get the Prometheus server URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=prometheus,app.kubernetes.io/instance=prometheus" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9090


The Prometheus alertmanager can be accessed via port 9093 on the following DNS name from within your cluster:
prometheus-alertmanager.default.svc.cluster.local


Get the Alertmanager URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=alertmanager,app.kubernetes.io/instance=prometheus" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9093
#################################################################################
######   WARNING: Pod Security Policy has been disabled by default since    #####
######            it deprecated after k8s 1.25+. use                        #####
######            (index .Values "prometheus-node-exporter" "rbac"          #####
###### .          "pspEnabled") with (index .Values                         #####
######            "prometheus-node-exporter" "rbac" "pspAnnotations")       #####
######            in case you still need it.                                #####
#################################################################################


The Prometheus PushGateway can be accessed via port 9091 on the following DNS name from within your cluster:
prometheus-prometheus-pushgateway.default.svc.cluster.local


Get the PushGateway URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus-pushgateway,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9091

For more information on running Prometheus, visit:
https://prometheus.io/
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get all
NAME                                                     READY   STATUS    RESTARTS   AGE
pod/prometheus-alertmanager-0                            1/1     Running   0          69s
pod/prometheus-kube-state-metrics-5cb7f5d847-8scpc       1/1     Running   0          69s
pod/prometheus-prometheus-node-exporter-ftw5m            1/1     Running   0          69s
pod/prometheus-prometheus-pushgateway-76465f5849-b4kpm   1/1     Running   0          69s
pod/prometheus-server-5dbdb658f9-zhxss                   1/2     Running   0          69s

NAME                                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
service/kubernetes                            ClusterIP   10.96.0.1       <none>        443/TCP    4d4h
service/prometheus-alertmanager               ClusterIP   10.105.104.1    <none>        9093/TCP   69s
service/prometheus-alertmanager-headless      ClusterIP   None            <none>        9093/TCP   69s
service/prometheus-kube-state-metrics         ClusterIP   10.99.190.239   <none>        8080/TCP   69s
service/prometheus-prometheus-node-exporter   ClusterIP   10.99.131.181   <none>        9100/TCP   69s
service/prometheus-prometheus-pushgateway     ClusterIP   10.111.84.177   <none>        9091/TCP   69s
service/prometheus-server                     ClusterIP   10.100.53.156   <none>        80/TCP     69s

NAME                                                 DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
daemonset.apps/prometheus-prometheus-node-exporter   1         1         1       1            1           kubernetes.io/os=linux   69s

NAME                                                READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/prometheus-kube-state-metrics       1/1     1            1           69s
deployment.apps/prometheus-prometheus-pushgateway   1/1     1            1           69s
deployment.apps/prometheus-server                   0/1     1            0           69s

NAME                                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/prometheus-kube-state-metrics-5cb7f5d847       1         1         1       69s
replicaset.apps/prometheus-prometheus-pushgateway-76465f5849   1         1         1       69s
replicaset.apps/prometheus-server-5dbdb658f9                   1         1         0       69s

NAME                                       READY   AGE
statefulset.apps/prometheus-alertmanager   1/1     69s
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
prometheus      default         1               2025-01-28 09:51:45.32745781 +0000 UTC  deployed        prometheus-27.1.0       v3.1.0     
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get pods
NAME                                                 READY   STATUS    RESTARTS   AGE
prometheus-alertmanager-0                            1/1     Running   0          13m
prometheus-kube-state-metrics-5cb7f5d847-8scpc       1/1     Running   0          13m
prometheus-prometheus-node-exporter-ftw5m            1/1     Running   0          13m
prometheus-prometheus-pushgateway-76465f5849-b4kpm   1/1     Running   0          13m
prometheus-se@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kube-state-metrics
bash: kube-state-metrics: command not found
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get svc
NAME                                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
kubernetes                            ClusterIP   10.96.0.1       <none>        443/TCP    4d4h
prometheus-alertmanager               ClusterIP   10.105.104.1    <none>        9093/TCP   16m
prometheus-alertmanager-headless      ClusterIP   None            <none>        9093/TCP   16m
prometheus-kube-state-metrics         ClusterIP   10.99.190.239   <none>        8080/TCP   16m
prometheus-prometheus-node-exporter   ClusterIP   10.99.131.181   <none>        9100/TCP   16m
prometheus-prometheus-pushgateway     ClusterIP   10.111.84.177   <none>        9091/TCP   16m
prometheus-server                     ClusterIP   10.100.53.156   <none>        80/TCP     16mrver-5dbdb658f9-zhxss                   2/2     Running   0          13m

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext
service/prometheus-server-ext exposed

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get svc
NAME                                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes                            ClusterIP   10.96.0.1       <none>        443/TCP        4d4h
prometheus-alertmanager               ClusterIP   10.105.104.1    <none>        9093/TCP       28m
prometheus-alertmanager-headless      ClusterIP   None            <none>        9093/TCP       28m
prometheus-kube-state-metrics         ClusterIP   10.99.190.239   <none>        8080/TCP       28m
prometheus-prometheus-node-exporter   ClusterIP   10.99.131.181   <none>        9100/TCP       28m
prometheus-prometheus-pushgateway     ClusterIP   10.111.84.177   <none>        9091/TCP       28m
prometheus-server                     ClusterIP   10.100.53.156   <none>        80/TCP         28m
prometheus-server-ext                 NodePort    10.101.118.16   <none>        80:30645/TCP   33s
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ minikube ip
192.168.49.2

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm repo add grafana https://grafana.github.io/helm-charts
"grafana" has been added to your repositories
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "grafana" chart repository
...Successfully got an update from the "prometheus-community" chart repository
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈Happy Helming!⎈@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm install grafana grafana/grafana
NAME: grafana
LAST DEPLOYED: Tue Jan 28 10:37:08 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get your 'admin' user password by running:

   kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo


2. The Grafana server can be accessed via port 80 on the following DNS name from within your cluster:

   grafana.default.svc.cluster.local

   Get the Grafana URL to visit by running these commands in the same shell:
     export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=grafana" -o jsonpath="{.items[0].metadata.name}")
     kubectl --namespace default port-forward $POD_NAME 3000

3. Login with the password from step 1 and the username: admin
#################################################################################
######   WARNING: Persistence is disabled!!! You will lose your data when   #####
######            the Grafana pod is terminated.                            #####
#################################################################################

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm repo add grafana https://grafana.github.io/helm-charts
"grafana" already exists with the same configuration, skipping
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "grafana" chart repository
...Successfully got an update from the "prometheus-community" chart repository
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈Happy Helming!⎈
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm install grafana grafana/grafana
Error: INSTALLATION FAILED: cannot re-use a name that is still in use
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
grafana         default         1               2025-01-28 10:37:08.672755093 +0000 UTC deployed        grafana-8.8.5           11.4.0     
prometheus      default         1               2025-01-28 09:51:45.32745781 +0000 UTC  deployed        prometheus-27.1.0       v3.1.0     

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
grafana         default         1               2025-01-28 10:37:08.672755093 +0000 UTC deployed        grafana-8.8.5           11.4.0     
prometheus      default         1               2025-01-28 09:51:45.32745781 +0000 UTC  deployed        prometheus-27.1.0       v3.1.0     
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get svc
NAME                                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
grafana                               ClusterIP   10.97.61.0      <none>        80/TCP         15m
grafana-ext                           NodePort    10.109.74.11    <none>        80:32689/TCP   11m
kubernetes                            ClusterIP   10.96.0.1       <none>        443/TCP        4d5h
prometheus-alertmanager               ClusterIP   10.105.104.1    <none>        9093/TCP       61m
prometheus-alertmanager-headless      ClusterIP   None            <none>        9093/TCP       61m
prometheus-kube-state-metrics         ClusterIP   10.99.190.239   <none>        8080/TCP       61m
prometheus-prometheus-node-exporter   ClusterIP   10.99.131.181   <none>        9100/TCP       61m
prometheus-prometheus-pushgateway     ClusterIP   10.111.84.177   <none>        9091/TCP       61m
prometheus-server                     ClusterIP   10.100.53.156   <none>        80/TCP         61m
prometheus-server-ext                 NodePort    10.101.118.16   <none>        80:30645/TCP   33m

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get secret --namespace default grafana -o jsonpath="{.data.grafana-admin-password}" | base64 --decode ; echo

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-ext
Error from server (AlreadyExists): services "grafana-ext" already exists

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get all
NAME                                                     READY   STATUS    RESTARTS   AGE
pod/grafana-7f47bb8f55-srqwb                             1/1     Running   0          24m
pod/prometheus-alertmanager-0                            1/1     Running   0          70m
pod/prometheus-kube-state-metrics-5cb7f5d847-8scpc       1/1     Running   0          70m
pod/prometheus-prometheus-node-exporter-ftw5m            1/1     Running   0          70m
pod/prometheus-prometheus-pushgateway-76465f5849-b4kpm   1/1     Running   0          70m
pod/prometheus-server-5dbdb658f9-zhxss                   2/2     Running   0          70m

NAME                                          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
service/grafana                               ClusterIP   10.97.61.0      <none>        80/TCP         24m
service/grafana-ext                           NodePort    10.109.74.11    <none>        80:32689/TCP   20m
service/kubernetes                            ClusterIP   10.96.0.1       <none>        443/TCP        4d5h
service/prometheus-alertmanager               ClusterIP   10.105.104.1    <none>        9093/TCP       70m
service/prometheus-alertmanager-headless      ClusterIP   None            <none>        9093/TCP       70m
service/prometheus-kube-state-metrics         ClusterIP   10.99.190.239   <none>        8080/TCP       70m
service/prometheus-prometheus-node-exporter   ClusterIP   10.99.131.181   <none>        9100/TCP       70m
service/prometheus-prometheus-pushgateway     ClusterIP   10.111.84.177   <none>        9091/TCP       70m
service/prometheus-server                     ClusterIP   10.100.53.156   <none>        80/TCP         70m
service/prometheus-server-ext                 NodePort    10.101.118.16   <none>        80:30645/TCP   42m

NAME                                                 DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR            AGE
daemonset.apps/prometheus-prometheus-node-exporter   1         1         1       1            1           kubernetes.io/os=linux   70m

NAME                                                READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/grafana                             1/1     1            1           24m
deployment.apps/prometheus-kube-state-metrics       1/1     1            1           70m
deployment.apps/prometheus-prometheus-pushgateway   1/1     1            1           70m
deployment.apps/prometheus-server                   1/1     1            1           70m

NAME                                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/grafana-7f47bb8f55                             1         1         1       24m
replicaset.apps/prometheus-kube-state-metrics-5cb7f5d847       1         1         1       70m
replicaset.apps/prometheus-prometheus-pushgateway-76465f5849   1         1         1       70m
replicaset.apps/prometheus-server-5dbdb658f9                   1         1         1       70m

NAME                                       READY   AGE
statefulset.apps/prometheus-alertmanager   1/1     70m
```
# install minkube on ubuntu
```
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
nstall minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100  119M  100  119M    0     0  35.1M      0  0:00:03  0:00:03 --:--:-- 51.5M
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ ls
Dockerfile  README.md  commands.txt  go.mod  hello.go
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
go-app       0.0.1     e761962cf2ea   12 minutes ago   15MB
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ minikube start
😄  minikube v1.35.0 on Ubuntu 20.04 (docker/amd64)
✨  Automatically selected the docker driver. Other choices: ssh, none
📌  Using Docker driver with root privileges
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.46 ...
💾  Downloading Kubernetes v1.32.0 preload ...
    > gcr.io/k8s-minikube/kicbase...:  500.31 MiB / 500.31 MiB  100.00% 40.30 M
    > preloaded-images-k8s-v18-v1...:  333.57 MiB / 333.57 MiB  100.00% 15.25 M
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED          SIZE
go-app                        0.0.1     e761962cf2ea   20 minutes ago   15MB
gcr.io/k8s-minikube/kicbase   v0.0.46   e72c4cbe9b29   2 weeks ago      1.31GB
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE                                 COMMAND                  CREATED         STATUS         PORTS                                                                                                                                  NAMES
beae4b343746   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   6 minutes ago   Up 6 minutes   127.0.0.1:32768->22/tcp, 127.0.0.1:32769->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32771->8443/tcp, 127.0.0.1:32772->32443/tcp   minikube
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl get node
NAME       STATUS   ROLES           AGE     VERSION
minikube   Ready    control-plane   6m53s   v1.32.0
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl cluster-info
Kubernetes control plane is running at https://192.168.49.2:8443
CoreDNS is running at https://192.168.49.2:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl get all
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   8m5s
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl get namespaces
NAME              STATUS   AGE
default           Active   9m4s
kube-node-lease   Active   9m4s
kube-public       Active   9m4s
kube-system       Active   9m4s
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl apply -f go-deploy.yaml 
deployment.apps/boardgame-deployment created
service/boardgame-service created
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl get pods
NAME                                    READY   STATUS              RESTARTS   AGE
boardgame-deployment-746775fb47-9hdft   0/1     ContainerCreating   0          13s
boardgame-deployment-746775fb47-wj7zk   0/1     ContainerCreating   0          13s
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl get all
NAME                                        READY   STATUS    RESTARTS   AGE
pod/boardgame-deployment-746775fb47-9hdft   1/1     Running   0          30s
pod/boardgame-deployment-746775fb47-wj7zk   1/1     Running   0          30s

NAME                        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
service/boardgame-service   NodePort    10.101.148.124   <none>        80:30980/TCP   30s
service/kubernetes          ClusterIP   10.96.0.1        <none>        443/TCP        14m

NAME                                   READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/boardgame-deployment   2/2     2            2           30s

NAME                                              DESIRED   CURRENT   READY   AGE
replicaset.apps/boardgame-deployment-746775fb47   2         2         2       30s
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl get pods -o wide
NAME                                    READY   STATUS    RESTARTS   AGE   IP           NODE       NOMINATED NODE   READINESS GATES
boardgame-deployment-746775fb47-9hdft   1/1     Running   0          56s   10.244.0.4   minikube   <none>           <none>
boardgame-deployment-746775fb47-wj7zk   1/1     Running   0          56s   10.244.0.3   minikube   <none>           <none>
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl describe pod boardgame-deployment-746775fb47-9hdft
Name:             boardgame-deployment-746775fb47-9hdft
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Thu, 30 Jan 2025 11:05:33 +0000
Labels:           app=boardgame
                  pod-template-hash=746775fb47
Annotations:      <none>
Status:           Running
IP:               10.244.0.4
IPs:
  IP:           10.244.0.4
Controlled By:  ReplicaSet/boardgame-deployment-746775fb47
Containers:
  boardgame:
    Container ID:   docker://c5eae132e1766936561a053539107fc6baac2998abb050ef7fedff559dd054b6
    Image:          owahed1/go-lang-app:0.0.2
    Image ID:       docker-pullable://owahed1/go-lang-app@sha256:60fd8bf7c535868a780235fda331c4eb576de7dff03d875a3b86773b27ac09ee
    Port:           8000/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Thu, 30 Jan 2025 11:05:51 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-7w2sm (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  kube-api-access-7w2sm:
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
  Normal  Scheduled  5m20s  default-scheduler  Successfully assigned default/boardgame-deployment-746775fb47-9hdft to minikube
  Normal  Pulling    5m19s  kubelet            Pulling image "owahed1/go-lang-app:0.0.2"
  Normal  Pulled     5m2s   kubelet            Successfully pulled image "owahed1/go-lang-app:0.0.2" in 2.028s (17.706s including waiting). Image size: 302971707 bytes.
  Normal  Created    5m2s   kubelet            Created container: boardgame
  Normal  Started    5m2s   kubelet            Started container boardgame

@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl describe deployments.apps boardgame-deployment 
Name:                   boardgame-deployment
Namespace:              default
CreationTimestamp:      Thu, 30 Jan 2025 11:05:33 +0000
Labels:                 <none>
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=boardgame
Replicas:               5 desired | 5 updated | 5 total | 5 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=boardgame
  Containers:
   boardgame:
    Image:         owahed1/go-lang-app:0.0.2
    Port:          8000/TCP
    Host Port:     0/TCP
    Environment:   <none>
    Mounts:        <none>
  Volumes:         <none>
  Node-Selectors:  <none>
  Tolerations:     <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Progressing    True    NewReplicaSetAvailable
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   boardgame-deployment-746775fb47 (5/5 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  10m    deployment-controller  Scaled up replica set boardgame-deployment-746775fb47 from 0 to 2
  Normal  ScalingReplicaSet  2m27s  deployment-controller  Scaled up replica set boardgame-deployment-746775fb47 from 2 to 5
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $ kubectl describe service boardgame-service 
Name:                     boardgame-service
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=boardgame
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.101.148.124
IPs:                      10.101.148.124
Port:                     <unset>  80/TCP
TargetPort:               8000/TCP
NodePort:                 <unset>  30980/TCP
Endpoints:                10.244.0.3:8000,10.244.0.4:8000,10.244.0.5:8000 + 2 more...
Session Affinity:         None
External Traffic Policy:  Cluster
Internal Traffic Policy:  Cluster
Events:                   <none>
@mir-owahed ➜ /workspaces/learn-linux/go-lang-app (main) $

Commands:
 1  docker images
    2  docker rmi go-app:multi
    3  docker ps
    4  docker build -t go-app:0.0.1 .
    5  docker images
    6  docker ps
    7  docker run --rm -p 8000:8000 go-app:0.0.1
    8  docker rmi go-app:multi
    9  docker rmi go-app:0.0.1
   10  docker build -t go-app:0.0.1 .
   11  docker images
   12  docker run --rm -p 8000:8000 go-app:0.0.1
   13  docker ps
   14  minikube status
   15  curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
   16  sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
   17  ls
   18  docker images
   19  docker ps
   20  minikube start
   21  docker images
   22  docker ps
   23  minikube status
   24  kubectl get node
   25  kubectl cluster-info
   26  kubectl get all
   27  kubectl get namespaces
   28  kubectl apply -f go-deploy.yaml 
   29  kubectl get pods
   30  kubectl get all
   31  kubectl get pods -o wide
   32  kubectl get pods pod/boardgame-deployment-746775fb47-9hdft
   33  kubectl describe pods pod/boardgame-deployment-746775fb47-9hdft
   34  kubectl describe pod pod/boardgame-deployment-746775fb47-9hdft
   35  kubectl describe pod boardgame-deployment-746775fb47-9hdft
   36  kubectl apply -f go-deploy.yaml 
   37  kubectl get pods -o wide
   38  kubectl get all
   39  kubectl describe deployments.apps boardgame-deployment 
   40  kubectl describe service boardgame-service 
   41  kubectl get pods
   42  kubectl describe pod boardgame-deployment-746775fb47-mdscb
   43  kubectl delete pod boardgame-deployment-746775fb47-mdscb
   44  kubectl get pods
   45  kubectl delete deployments.apps boardgame-deployment 
   46  kubectl get pods
   47  kubectl get all
   48  minikube stop
   49  history
```






