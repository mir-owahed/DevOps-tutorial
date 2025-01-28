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
```







