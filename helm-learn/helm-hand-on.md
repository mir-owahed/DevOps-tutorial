```
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm version
version.BuildInfo{Version:"v3.16.3", GitCommit:"cfd07493f46efc9debd9cc1b02a0961186df7fdf", GitTreeState:"clean", GoVersion:"go1.22.7"}
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm repo ls
Error: no repositories to show
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm repo add https://charts.bitnami.com/bitnami
Error: "helm repo add" requires 2 arguments

Usage:  helm repo add [NAME] [URL] [flags]
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm repo add bitnami https://charts.bitnami.com/bitnami
"bitnami" has been added to your repositories
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm repo ls
NAME    URL                               
bitnami https://charts.bitnami.com/bitnami
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm list --all-name-spaces
Error: unknown flag: --all-name-spaces
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm list --all-namespaces
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm search repo ngins
No results found
@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ helm search repo nginx
NAME                                    CHART VERSION   APP VERSION     DESCRIPTION                                       
bitnami/nginx                           18.3.5          1.27.3          NGINX Open Source is a web server that can be a...
bitnami/nginx-ingress-controller        11.6.5          1.12.0          NGINX Ingress Controller is an Ingress controll...
bitnami/nginx-intel                     2.1.15          0.4.9           DEPRECATED NGINX Open Source for Intel is a lig...

@mir-owahed ➜ /workspaces/learn-linux-lab/python-example (main) $ curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
@mir-owahed ➜ ~/helm-learn $ helm repo search nginx
@mir-owahed ➜ ~/helm-learn $ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ ~/helm-learn $ helm repo ls
NAME    URL                               
bitnami https://charts.bitnami.com/bitnami
@mir-owahed ➜ ~/helm-learn $ helm repo search nginx
@mir-owahed ➜ ~/helm-learn $ helm search repo nginx
NAME                                    CHART VERSION   APP VERSION     DESCRIPTION                                       
bitnami/nginx                           18.3.5          1.27.3          NGINX Open Source is a web server that can be a...
bitnami/nginx-ingress-controller        11.6.5          1.12.0          NGINX Ingress Controller is an Ingress controll...
bitnami/nginx-intel                     2.1.15          0.4.9           DEPRECATED NGINX Open Source for Intel is a lig...
@mir-owahed ➜ ~/helm-learn $ hel
helm       help       helpztags  
@mir-owahed ➜ ~/helm-learn $ helm install webserver bitnami/n
bitnami/nats                      bitnami/nessie                    bitnami/nginx-ingress-controller  bitnami/node                      
bitnami/neo4j                     bitnami/nginx                     bitnami/nginx-intel               bitnami/node-exporter             
@mir-owahed ➜ ~/helm-learn $ helm install webserver bitnami/nginx
NAME: webserver
LAST DEPLOYED: Fri Jan 24 05:51:05 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: nginx
CHART VERSION: 18.3.5
APP VERSION: 1.27.3

Did you know there are enterprise versions of the Bitnami catalog? For enhanced secure software supply chain features, unlimited pulls from Docker, LTS support, or application customization, see Bitnami Premium or Tanzu Application Catalog. See https://www.arrow.com/globalecs/na/vendors/bitnami for more information.

** Please be patient while the chart is being deployed **
NGINX can be accessed through the following DNS name from within your cluster:

    webserver-nginx.default.svc.cluster.local (port 80)

To access NGINX from outside the cluster, follow the steps below:

1. Get the NGINX URL by running these commands:

  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        Watch the status with: 'kubectl get svc --namespace default -w webserver-nginx'

    export SERVICE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].port}" services webserver-nginx)
    export SERVICE_IP=$(kubectl get svc --namespace default webserver-nginx -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
    echo "http://${SERVICE_IP}:${SERVICE_PORT}"

WARNING: There are "resources" sections in the chart not set. Using "resourcesPreset" is not recommended for production. For production installations, please set the following values according to your workload needs:
  - cloneStaticSiteFromGit.gitSync.resources
  - resources
+info https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
@mir-owahed ➜ ~/helm-learn $ 
```
