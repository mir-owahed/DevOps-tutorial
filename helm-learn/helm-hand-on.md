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
## helm hands-on Minikube
```
mir@ubuntu-vbox:~$ minikube start

😄  minikube v1.35.0 on Ubuntu 22.04 (vbox/amd64)

✨  Using the docker driver based on existing profile

👍  Starting "minikube" primary control-plane node in "minikube" cluster

🚜  Pulling base image v0.0.46 ...

🔄  Restarting existing docker container for "minikube" ...



🧯  Docker is nearly out of disk space, which may cause deployments to fail! (89% of capacity). You can pass '--force' to skip this check.

💡  Suggestion: 



    Try one or more of the following to free up space on the device:

    

    1. Run "docker system prune" to remove unused Docker data (optionally with "-a")

    2. Increase the storage allocated to Docker for Desktop by clicking on:

    Docker icon > Preferences > Resources > Disk Image Size

    3. Run "minikube ssh -- docker system prune" if using the Docker container runtime

🍿  Related issue: https://github.com/kubernetes/minikube/issues/9024



❗  Failing to connect to https://registry.k8s.io/ from inside the minikube container

💡  To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/

🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...

🔎  Verifying Kubernetes components...

    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5

🌟  Enabled addons: storage-provisioner, default-storageclass

🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

mir@ubuntu-vbox:~$ helm version

version.BuildInfo{Version:"v3.17.0", GitCommit:"301108edc7ac2a8ba79e4ebf5701b0b6ce6a31e4", GitTreeState:"clean", GoVersion:"go1.23.4"}

mir@ubuntu-vbox:~$ helm

The Kubernetes package manager



Common actions for Helm:



- helm search:    search for charts

- helm pull:      download a chart to your local directory to view

- helm install:   upload the chart to Kubernetes

- helm list:      list releases of charts



Environment variables:



| Name                               | Description                                                                                                |

|------------------------------------|------------------------------------------------------------------------------------------------------------|

| $HELM_CACHE_HOME                   | set an alternative location for storing cached files.                                                      |

| $HELM_CONFIG_HOME                  | set an alternative location for storing Helm configuration.                                                |

| $HELM_DATA_HOME                    | set an alternative location for storing Helm data.                                                         |

| $HELM_DEBUG                        | indicate whether or not Helm is running in Debug mode                                                      |

| $HELM_DRIVER                       | set the backend storage driver. Values are: configmap, secret, memory, sql.                                |

| $HELM_DRIVER_SQL_CONNECTION_STRING | set the connection string the SQL storage driver should use.                                               |

| $HELM_MAX_HISTORY                  | set the maximum number of helm release history.                                                            |

| $HELM_NAMESPACE                    | set the namespace used for the helm operations.                                                            |

| $HELM_NO_PLUGINS                   | disable plugins. Set HELM_NO_PLUGINS=1 to disable plugins.                                                 |

| $HELM_PLUGINS                      | set the path to the plugins directory                                                                      |

| $HELM_REGISTRY_CONFIG              | set the path to the registry config file.                                                                  |

| $HELM_REPOSITORY_CACHE             | set the path to the repository cache directory                                                             |

| $HELM_REPOSITORY_CONFIG            | set the path to the repositories file.                                                                     |

| $KUBECONFIG                        | set an alternative Kubernetes configuration file (default "~/.kube/config")                                |

| $HELM_KUBEAPISERVER                | set the Kubernetes API Server Endpoint for authentication                                                  |

| $HELM_KUBECAFILE                   | set the Kubernetes certificate authority file.                                                             |

| $HELM_KUBEASGROUPS                 | set the Groups to use for impersonation using a comma-separated list.                                      |

| $HELM_KUBEASUSER                   | set the Username to impersonate for the operation.                                                         |

| $HELM_KUBECONTEXT                  | set the name of the kubeconfig context.                                                                    |

| $HELM_KUBETOKEN                    | set the Bearer KubeToken used for authentication.                                                          |

| $HELM_KUBEINSECURE_SKIP_TLS_VERIFY | indicate if the Kubernetes API server's certificate validation should be skipped (insecure)                |

| $HELM_KUBETLS_SERVER_NAME          | set the server name used to validate the Kubernetes API server certificate                                 |

| $HELM_BURST_LIMIT                  | set the default burst limit in the case the server contains many CRDs (default 100, -1 to disable)         |

| $HELM_QPS                          | set the Queries Per Second in cases where a high number of calls exceed the option for higher burst values |



Helm stores cache, configuration, and data based on the following configuration order:



- If a HELM_*_HOME environment variable is set, it will be used

- Otherwise, on systems supporting the XDG base directory specification, the XDG variables will be used

- When no other location is set a default location will be used based on the operating system



By default, the default directories depend on the Operating System. The defaults are listed below:



| Operating System | Cache Path                | Configuration Path             | Data Path               |

|------------------|---------------------------|--------------------------------|-------------------------|

| Linux            | $HOME/.cache/helm         | $HOME/.config/helm             | $HOME/.local/share/helm |

| macOS            | $HOME/Library/Caches/helm | $HOME/Library/Preferences/helm | $HOME/Library/helm      |

| Windows          | %TEMP%\helm               | %APPDATA%\helm                 | %APPDATA%\helm          |



Usage:

  helm [command]



Available Commands:

  completion  generate autocompletion scripts for the specified shell

  create      create a new chart with the given name

  dependency  manage a chart's dependencies

  env         helm client environment information

  get         download extended information of a named release

  help        Help about any command

  history     fetch release history

  install     install a chart

  lint        examine a chart for possible issues

  list        list releases

  package     package a chart directory into a chart archive

  plugin      install, list, or uninstall Helm plugins

  pull        download a chart from a repository and (optionally) unpack it in local directory

  push        push a chart to remote

  registry    login to or logout from a registry

  repo        add, list, remove, update, and index chart repositories

  rollback    roll back a release to a previous revision

  search      search for a keyword in charts

  show        show information of a chart

  status      display the status of the named release

  template    locally render templates

  test        run tests for a release

  uninstall   uninstall a release

  upgrade     upgrade a release

  verify      verify that a chart at the given path has been signed and is valid

  version     print the client version information



Flags:

      --burst-limit int                 client-side default throttling limit (default 100)

      --debug                           enable verbose output

  -h, --help                            help for helm

      --kube-apiserver string           the address and the port for the Kubernetes API server

      --kube-as-group stringArray       group to impersonate for the operation, this flag can be repeated to specify multiple groups.

      --kube-as-user string             username to impersonate for the operation

      --kube-ca-file string             the certificate authority file for the Kubernetes API server connection

      --kube-context string             name of the kubeconfig context to use

      --kube-insecure-skip-tls-verify   if true, the Kubernetes API server's certificate will not be checked for validity. This will make your HTTPS connections insecure

      --kube-tls-server-name string     server name to use for Kubernetes API server certificate validation. If it is not provided, the hostname used to contact the server is used

      --kube-token string               bearer token used for authentication

      --kubeconfig string               path to the kubeconfig file

  -n, --namespace string                namespace scope for this request

      --qps float32                     queries per second used when communicating with the Kubernetes API, not including bursting

      --registry-config string          path to the registry config file (default "/home/mir/.config/helm/registry/config.json")

      --repository-cache string         path to the directory containing cached repository indexes (default "/home/mir/.cache/helm/repository")

      --repository-config string        path to the file containing repository names and URLs (default "/home/mir/.config/helm/repositories.yaml")



Use "helm [command] --help" for more information about a command.

mir@ubuntu-vbox:~$ helm repo list

NAME   	URL                               

bitnami	https://charts.bitnami.com/bitnami
mir@ubuntu-vbox:~$ helm list

NAME	NAMESPACE	REVISION	UPDATED	STATUS	CHART	APP VERSION

```
## Install wordpress
```
mir@ubuntu-vbox:~/helm-wordpress$ helm list
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHA
mir@ubuntu-vbox:~/helm-wordpress$ helm repo ls
NAME    URL                               
bitnami https://charts.bitnami.com/bitnami
mir@ubuntu-vbox:~/helm-wordpress$ helm install test-wordpress bitnami/wordpress --version 24.1.7 --values=wordpress-values.yml
NAME: test-wordpress
LAST DEPLOYED: Sat Jan 25 22:18:26 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: wordpress
CHART VERSION: 24.1.7
APP VERSION: 6.7.1

Did you know there are enterprise versions of the Bitnami catalog? For enhanced secure software supply chain features, unlimited pulls from Docker, LTS support, or application customization, see Bitnami Premium or Tanzu Application Catalog. See https://www.arrow.com/globalecs/na/vendors/bitnami for more information.

** Please be patient while the chart is being deployed **

Your WordPress site can be accessed through the following DNS name from within your cluster:

    test-wordpress.default.svc.cluster.local (port 80)

To access your WordPress site from outside the cluster follow the steps below:

1. Get the WordPress URL by running these commands:

  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        Watch the status with: 'kubectl get svc --namespace default -w test-wordpress'

   export SERVICE_IP=$(kubectl get svc --namespace default test-wordpress --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")
   echo "WordPress URL: http://$SERVICE_IP/"
   echo "WordPress Admin URL: http://$SERVICE_IP/admin"
mir@ubuntu-vbox:~/helm-wordpress$ kubectl get all
NAME                                  READY   STATUS    RESTARTS      AGE
pod/goapp-5d886579d9-x25dw            1/1     Running   2 (30m ago)   22h
pod/test-wordpress-5697d9c5fc-sk5z6   1/1     Running   0             3m15s
pod/test-wordpress-mariadb-0          1/1     Running   0             3m15s

NAME                                      TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
service/kubernetes                        ClusterIP      10.96.0.1       <none>        443/TCP                      2d2h
service/test-wordpress                    LoadBalancer   10.110.169.49   <pending>     80:31255/TCP,443:30504/TCP   3m15s
service/test-wordpress-mariadb            ClusterIP      10.99.28.29     <none>        3306/TCP                     3m15s
service/test-wordpress-mariadb-headless   ClusterIP      None            <none>        3306/TCP                     3m15s
mir@ubuntu-vbox:~/helm-wordpress$ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
test-wordpress  default         1               2025-01-25 22:18:26.183204899 +0530 IST deployed        wordpress-24.1.7        6.7.1      
mir@ubuntu-vbox:~/helm-wordpress$ helm upgrade test-wordpress bitnami/wordpress --values=wordpress-values.yml
Release "test-wordpress" has been upgraded. Happy Helming!
NAME: test-wordpress
LAST DEPLOYED: Sat Jan 25 22:28:18 2025
NAMESPACE: default
STATUS: deployed
REVISION: 2
TEST SUITE: None
NOTES:
CHART NAME: wordpress
CHART VERSION: 24.1.7
APP VERSION: 6.7.1

mir@ubuntu-vbox:~/helm-wordpress$ helm ls
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
test-wordpress  default         2               2025-01-25 22:28:18.473076685 +0530 IST deployed        wordpress-24.1.7        6.7.1      
     
mir@ubuntu-vbox:~/helm-wordpress$ kubectl get all
NAME                                  READY   STATUS    RESTARTS      AGE
pod/goapp-5d886579d9-x25dw            1/1     Running   2 (40m ago)   22h
pod/test-wordpress-5697d9c5fc-sk5z6   1/1     Running   0             13m
pod/test-wordpress-5b478678d9-nwx48   0/1     Pending   0             3m50s
pod/test-wordpress-mariadb-0          1/1     Running   0             13m

NAME                                      TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
service/kubernetes                        ClusterIP      10.96.0.1       <none>        443/TCP                      2d2h
service/test-wordpress                    LoadBalancer   10.110.169.49   <pending>     80:31255/TCP,443:30504/TCP   13m
service/test-wordpress-mariadb            ClusterIP      10.99.28.29     <none>        3306/TCP                     13m
service/test-wordpress-mariadb-headless   ClusterIP      None            <none>        3306/TCP                     13m

NAME                             READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/goapp            1/1     1            1           22h
deployment.apps/test-wordpress   1/1     1            1           13m

NAME                                        DESIRED   CURRENT   READY   AGE
replicaset.apps/goapp-5d886579d9            1         1         1       22h
replicaset.apps/test-wordpress-5697d9c5fc   1         1         1       13m
replicaset.apps/test-wordpress-5b478678d9   1         1         0       3m50s

NAME                                      READY   AGE
statefulset.apps/test-wordpress-mariadb   1/1     13m

mir@ubuntu-vbox:~/helm-wordpress$ helm history test-wordpress
REVISION        UPDATED                         STATUS          CHART                   APP VERSION     DESCRIPTION     
1               Sat Jan 25 22:18:26 2025        superseded      wordpress-24.1.7        6.7.1           Install complete
2               Sat Jan 25 22:28:18 2025        deployed        wordpress-24.1.7        6.7.1           Upgrade complete

```
# Deploy Go app on Minikube Cluster using helm chart
```minikube start

  helm ls
mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ docker build -t go-app:letest .
[+] Building 74.0s (9/9) FINISHED                                                                          docker:default
 => [internal] load build definition from Dockerfile                                                                 0.2s
 => => transferring dockerfile: 163B                                                                                 0.0s
 => [internal] load metadata for docker.io/library/golang:1.22-alpine                                               13.2s
 => [internal] load .dockerignore                                                                                    0.1s
 => => transferring context: 2B                                                                                      0.0s
 => [1/4] FROM docker.io/library/golang:1.22-alpine@sha256:161858498a61ce093c8e2bd704299bfb23e5bff79aef99b6c40bb9c  38.0s
 => => resolve docker.io/library/golang:1.22-alpine@sha256:161858498a61ce093c8e2bd704299bfb23e5bff79aef99b6c40bb9c6  0.1s
 => => sha256:95c2bb3c66000349add42940791d5cf80b25f5b007113d83f0b48cb719333b02 1.92kB / 1.92kB                       0.0s
mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ helm create 
mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED          SIZE
go-app                        letest    62c93ed955e5   15 minutes ago   304MB
hello-world                   latest    74cc54e27dc4   4 days ago       10.1kB
gcr.io/k8s-minikube/kicbase   v0.0.46   e72c4cbe9b29   12 days ago      1.31GB
mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ helm list
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ helm install myapp-chart go-app-chart
NAME: myapp-chart
LAST DEPLOYED: Sun Jan 26 10:40:01 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services myapp-chart-go-app-chart)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT

mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ kubectl get all
NAME                                           READY   STATUS             RESTARTS      AGE
pod/goapp-5d886579d9-x25dw                     1/1     Running            3 (56m ago)   34h
pod/myapp-chart-go-app-chart-df8dd9dd6-tkqqz   0/1     ErrImagePull       0             5m4s
pod/myapp-chart-go-app-chart-df8dd9dd6-vrv7b   0/1     ImagePullBackOff   0             5m4s
pod/myapp-chart-go-app-chart-df8dd9dd6-vww66   0/1     ImagePullBackOff   0             5m4s

NAME                               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/kubernetes                 ClusterIP   10.96.0.1        <none>        443/TCP          2d14h
service/myapp-chart-go-app-chart   NodePort    10.101.164.221   <none>        8000:31886/TCP   5m4s

NAME                                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/goapp                      1/1     1            1           34h
deployment.apps/myapp-chart-go-app-chart   0/3     3            0           5m4s

NAME                                                 DESIRED   CURRENT   READY   AGE
replicaset.apps/goapp-5d886579d9                     1         1         1       34h
replicaset.apps/myapp-chart-go-app-chart-df8dd9dd6   3         3         0       5m4s

mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ kubectl get pods
NAME                                       READY   STATUS             RESTARTS      AGE
goapp-5d886579d9-x25dw                     1/1     Running            3 (58m ago)   34h
myapp-chart-go-app-chart-df8dd9dd6-tkqqz   0/1     ImagePullBackOff   0             6m54s
myapp-chart-go-app-chart-df8dd9dd6-vrv7b   0/1     ImagePullBackOff   0             6m54s
myapp-chart-go-app-chart-df8dd9dd6-vww66   0/1     ImagePullBackOff   0             6m54s
mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ kubectl get svc
NAME                       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
kubernetes                 ClusterIP   10.96.0.1        <none>        443/TCP          2d14h
myapp-chart-go-app-chart   NodePort    10.101.164.221   <none>        8000:31886/TCP   7m27s

mir@ubuntu-vbox:~/helm-wordpress/go-lang-app$ helm list
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART             APP VERSION
myapp-chart     default         1               2025-01-26 10:40:01.749274825 +0530 IST deployed        go-app-chart-0.1.01.16.0     
```
## helm hands-on at GitHub Codespaces
```
@mir-owahed ➜ ~/helm-learn $ helm version
version.BuildInfo{Version:"v3.16.3", GitCommit:"cfd07493f46efc9debd9cc1b02a0961186df7fdf", GitTreeState:"clean", GoVersion:"go1.22.7"}
@mir-owahed ➜ ~/helm-learn $ helm list
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ ~/helm-learn $ git clone https://github.com/mir-owahed/go-lang-app.git
Cloning into 'go-lang-app'...
remote: Enumerating objects: 27, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (26/26), done.
remote: Total 27 (delta 10), reused 9 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (27/27), 7.40 KiB | 7.40 MiB/s, done.
Resolving deltas: 100% (10/10), done.
@mir-owahed ➜ ~/helm-learn $ ls
go-lang-app
@mir-owahed ➜ ~/helm-learn $ cd go-lang-app/
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ code .
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl version
Client Version: v1.32.0
Kustomize Version: v5.5.0
Server Version: v1.32.0
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get all
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   2d23h

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED       SIZE
gcr.io/k8s-minikube/kicbase   v0.0.46   e72c4cbe9b29   13 days ago   1.31GB
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ free 
              total        used        free      shared  buff/cache   available
Mem:        8119864     2214316      308596       72840     5596952     5510296
Swap:             0           0           0
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ free -h
              total        used        free      shared  buff/cache   available
Mem:          7.7Gi       2.1Gi       293Mi        71Mi       5.3Gi       5.2Gi
Swap:            0B          0B          0B
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay          32G   14G   17G  47% /
tmpfs            64M     0   64M   0% /dev
shm              64M     0   64M   0% /dev/shm
/dev/root        29G   24G  5.2G  83% /vscode
/dev/sda1        44G   22G   21G  51% /tmp
/dev/loop4       32G   14G   17G  47% /workspaces
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker build -t g-app:latest .
[+] Building 34.3s (10/10) FINISHED
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE                                 COMMAND                  CREATED      STATUS          PORTS                                                                                                                                  NAMES
15848f652909   gcr.io/k8s-minikube/kicbase:v0.0.46   "/usr/local/bin/entr…"   3 days ago   Up 27 minutes   127.0.0.1:32768->22/tcp, 127.0.0.1:32769->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32771->8443/tcp, 127.0.0.1:32772->32443/tcp   minikube
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker run --rm -p 8000:8000 g-app:latest
Mir's server is now running
/ping endpoint was invoked
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED          SIZE
g-app                         latest    2d000a23a07f   11 minutes ago   304MB
gcr.io/k8s-minikube/kicbase   v0.0.46   e72c4cbe9b29   13 days ago      1.31GB
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm create go-app-chart
Creating go-app-chart
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ ls
Dockerfile  README.md  commands.txt  dockerfile.multi  go-app-chart  go.mod  hello.go
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm install go-app go-app-chart/
NAME: go-app
LAST DEPLOYED: Mon Jan 27 05:36:12 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services go-app-go-app-chart)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
go-app  default         1               2025-01-27 05:36:12.325569941 +0000 UTC deployed        go-app-chart-0.1.0      1.16.0     
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ kubectl get all
NAME                                      READY   STATUS             RESTARTS   AGE
pod/go-app-go-app-chart-8f6669cd4-xqdq6   0/1     ImagePullBackOff   0          2m9s

NAME                          TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)          AGE
service/go-app-go-app-chart   NodePort    10.98.69.60   <none>        8000:30742/TCP   2m9s
service/kubernetes            ClusterIP   10.96.0.1     <none>        443/TCP          3d

NAME                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/go-app-go-app-chart   0/1     1            0           2m9s

NAME                                            DESIRED   CURRENT   READY   AGE
replicaset.apps/go-app-go-app-chart-8f6669cd4   1         1         0       2m9s
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
go-app  default         1               2025-01-27 05:36:12.325569941 +0000 UTC deployed        go-app-chart-0.1.0      1.16.0     
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm status go-app
NAME: go-app
LAST DEPLOYED: Mon Jan 27 05:36:12 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services go-app-go-app-chart)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
go-app  default         1               2025-01-27 05:36:12.325569941 +0000 UTC deployed        go-app-chart-0.1.0      1.16.0     
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm upgrade go-app go-app-chart/
Release "go-app" has been upgraded. Happy Helming!
NAME: go-app
LAST DEPLOYED: Mon Jan 27 05:53:26 2025
NAMESPACE: default
STATUS: deployed
REVISION: 2
NOTES:
1. Get the application URL by running these commands:
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services go-app-go-app-chart)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT

@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
go-app  default         2               2025-01-27 05:53:26.702565453 +0000 UTC deployed        go-app-chart-0.1.0      1.16.0
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm rollback go-app 1
Rollback was a success! Happy Helming!
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
go-app  default         3               2025-01-27 06:08:49.281279931 +0000 UTC deployed        go-app-chart-0.1.0      1.16.0
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
go-app  default         3               2025-01-27 06:08:49.281279931 +0000 UTC deployed        go-app-chart-0.1.0      1.16.0     
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm history go-app 
REVISION        UPDATED                         STATUS          CHART                   APP VERSION     DESCRIPTION     
1               Mon Jan 27 05:36:12 2025        superseded      go-app-chart-0.1.0      1.16.0          Install complete
2               Mon Jan 27 05:53:26 2025        superseded      go-app-chart-0.1.0      1.16.0          Upgrade complete
3               Mon Jan 27 06:08:49 2025        deployed        go-app-chart-0.1.0      1.16.0          Rollback to 1
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm uninstall go-app --keep-history
release "go-app" uninstalled
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm ls
NAME    NAMESPACE       REVISION        UPDATED STATUS  CHART   APP VERSION
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm history go-app
REVISION        UPDATED                         STATUS          CHART                   APP VERSION     DESCRIPTION            
1               Mon Jan 27 05:36:12 2025        superseded      go-app-chart-0.1.0      1.16.0          Install complete       
2               Mon Jan 27 05:53:26 2025        superseded      go-app-chart-0.1.0      1.16.0          Upgrade complete       
3               Mon Jan 27 06:08:49 2025        uninstalled     go-app-chart-0.1.0      1.16.0          Uninstallation complete
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm uninstall go-app 
release "go-app" uninstalled
@mir-owahed ➜ ~/helm-learn/go-lang-app (main) $ helm history go-app
Error: release: not found
```





