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

