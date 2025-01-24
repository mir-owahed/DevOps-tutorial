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
```
