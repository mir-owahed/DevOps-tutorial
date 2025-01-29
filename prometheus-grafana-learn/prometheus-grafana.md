## install Prometheus on k8s
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
