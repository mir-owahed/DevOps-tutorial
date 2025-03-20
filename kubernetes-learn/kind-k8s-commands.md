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
```
mir@DESKTOP-JASRD4A:~$ history
    1  df -H
    2  free -H
    3  free
    4  sudo apt update
    5  mkdir test
    6  cd test
    7  code .
    8  du -H
    9  df -H
   10  free
   11  free -H
   12  free -h
   13  go version
   14  cd
   15  ls
   16  cd test
   17  code .
   18  cd
   19  docker ps
   20  ls
   21  wget https://go.dev/dl/go1.24.1.linux-amd64.tar.gz
   22  ls
   23  rm -rf /usr/local/go
   24  tar -C /usr/local -xzf go1.24.1.linux-amd64.tar.gz
   25  ls -la
   26  sudo nano .bashrc
   27  go version
   28  git clone https://github.com/mir-owahed/ultimate-devops-project-demo.git
   29  ls
   30  cd ultimate-devops-project-demo/
   31  ls
   32  cd src/
   33  ls
   34  cd ad/
   35  ls
   36  cd ..
   37  ls
   38  cd product-catalog/
   39  ls
   40  go version
   41  restart
   42  reboot
   43  go version
   44  ls
   45  sudo rm -rf /usr/local/go
   46  ls
   47  sudo tar -C /usr/local -xzf go1.24.1.linux-amd64.tar.gz
   48  sudo nano $HOME/.profile
   49  sudo  source $HOME/.profile
   50  source $HOME/.profile
   51  go version
   52  ls
   53  rm go1.24.1.linux-amd64.tar.gz
   54  ls
   55  cd ultimate-devops-project-demo/
   56  cd src/product-catalog/
   57  ls
   58  go mod download
   59  go build -o product-catalog .
   60  ls
   61  ./prod
   62  ./product-catalog
   63  google-chrome
   64  sudo apt install google-chrome
   65  google-chrome
   66  cd /tmp
   67  wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
   68  sudo apt install --fix-missing ./google-chrome-stable_current_amd64.deb
   69  google-chrome
   70  cd
   71  ls
   72  google-chrome
   73  java --version
   74  sudo apt install openjdk-21-jdk -y
   75  java --version
   76  cd ultimate-devops-project-demo/
   77  cd src/
   78  ls
   79  cd ad/
   80  ls
   81  ls -la
   82  ./gradlew
   83  ./gradlew installDist
   84  export AD_PORT=8080
   85  export FEATURE_FLAG_GRPC_SERVICE_ADDR=featureflagservice:50053
   86  ./build/install/opentelemetry-demo-ad/bin/Ad
   87  ls
   88  cd build/install/opentelemetry-demo-ad/bin/
   89  ls
   90  cd
   91  git clone https://github.com/open-telemetry/opentelemetry-demo.git
   92  cd opentelemetry-demo/
   93  ls
   94  cd src/ad/
   95  ls
   96  ls -la
   97  ./gradlew
   98  ./gradlew installDist
   99  node -v
  100  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
  101  ls
  102  cd
  103  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
  104  ls
  105  git clone https://github.com/mir-owahed/devsecops-demo.git
  106  cd devsecops-demo/
  107  ls
  108  code .
  109  cd
  110  nvm install node
  111  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
  112  nvm install node
  113  curl localhost:5137
  114  curl http://localhost:5137/
  115  curl http://localhost:5137
  116  npm start
  117  npm install
  118  npm start
  119  npm run start
  120  npm run dev
  121  npm run build
  122  npm start
  123  npm install
  124  npm run dev
  125  npm ci
  126  npm run grpc:generate
  127  npm start
  128  node -v
  129  npm -v
  130  cd devsecops-demo/
  131  ls
  132  code .
  133  ls
  134  cd
  135  ls
  136  cd ultimate-devops-project-demo/
  137  ls
  138  cd src/
  139  ls
  140  cd frontend
  141  ls
  142  code .
  143  ls
  144  docker ps
  145  vim install_docker.sh
  146  ls
  147  sudo chmod +x install_docker.sh
  148  ls
  149  ./install_docker.sh
  150  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  151  ls
  152  docker version
  153  sudo usermod -aG $USER
  154  sudo usermod -aG docker $USER
  155  docker version
  156  kubectl create deployment nginx --image nginx
  157  kubectl get pods -w
  158  kubectl get all
  159  kubectl port-forward pod/nginx-5869d7778c-fvv49 8989:80
  160  docker ps
  161  pwd
  162  # For AMD64 / x86_64
  163  [ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-amd64
  164  # For ARM64
  165  [ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-arm64
  166  chmod +x ./kind
  167  sudo mv ./kind /usr/local/bin/kind
  168  ls
  169  kind version
  170  kind create cluster 1-node-k8s
  171  kind create cluster --name 1-node-k8s
  172  kind get cluster
  173  kind get clusters
  174  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  175  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
  176  kubectl version --client
  177  kubectl config current-context
  178  mkdir k8s
  179  cd k8s/
  180  code .
  181  docker ps
  182  kubectl gets pods
  183  kubectl get pods
  184  nano multinode-cluster.yaml
  185  kind create cluster --name 9-node-k8s --config=multinode-cluster.yaml
  186  kubectl config current-context
  187  kubectl get clusters
  188  kubectl get cluster
  189  kind get clusters
  190  kind delete cluster
  191  kind get clusters
  192  kind delete cluster 1-node-k8s
  193  kind delete cluster --name 1-node-k8s
  194  kind delete cluster --name 9-node-k8s
  195  history
  196  cd
  197  npm run start
  198  npm run build
  199  sudo apt install nginx
  200  sudo cp -r build/* /var/www/html/
  201  sudo restart nginx
  202  sudo systectl restart nginx
  203  sudo systemctl restart nginx
  204  npm run build
  205  sudo cp -r build/* /var/www/html/
  206  sudo systemctl restart nginx
  207  npm run server
  208  npm run serve
  209  npm run deploy
  210  ls
  211  kind clusters-info
  212  kind get clusters
  213  docker ps
  214  docker ps -a
  215  node -v
  216  npm -v
  217  npx create-docusaurus@latest my-website classic
  218  cd my-website/
  219  code .
  220  ls
  221  kind version
  222  minikube status
  223  kubectl cluster-info
  224  kind get nodes
  225  kind get clusters
  226  ls
  227  nano kind-multi-cluster-info.yaml
  228  ls
  229  kind create cluster --config kind-multi-cluster-info.yaml --name 3-node-kind-cluster
  230  kubectl cluster-info
  231  kind get clusters
  232  kubectl config current-context
  233  kind get nodes
  234  kubectl get nodes
  235  docker ps
  236  docker ps -a
  237  ls
  238  nano go-app-deployment.yaml
  239  kubectl apply -f go-app-deployment.yaml
  240  kubectl get pods -w
  241  docker ps
  242  kubectl get pods
  243  kubectl get all
  244  kubectl port-forward service/goapp-service 8989:8000
  245  kubectl port-forward service/goapp-service 8989:80
  246  ls
  247  cls
  248  clear
  249  ls
  250  kubectl create namespace argocd
  251  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  252  kubectl get pods -n argocd
  253  kubectl get pods -n argocd -w
  254  kubectl get pods -n argocd
  255  kubectl port-forward svc/argocd-server -n argocd 8080:80
  256  kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
  257  kubectl port-forward svc/argocd-server -n argocd 8080:80
  258  kubectl get pods -n argocd
  259  kubectl get pods
  260  kubectl port-forward goapp-deployment-67776fc699-9z9ms 3700:80
  261  kubectl port-forward goapp-deployment-67776fc699-9z9ms 8585:80
  262  kubectl get all
  263  kubectl get nodes
  264  kubectl config current-context
  265  kubectl delete cluster --name kind-3-node-kind-cluster
  266  kubectl delete cluster --name=kind-3-node-kind-cluster
  267  kind  delete cluster
  268  kind delete cluster --name=kind-3-node-kind-cluster
  269  docker ps
  270  kubectl get nodes
  271  kubectl confif current-context
  272  kubectl config current-context
  273  kind get clusters
  274  kubectl get pods
  275  kubectl get all
  276  kubectl delete deployment deployment.apps/goapp-deployment
  277  kubectl delete deployment.apps/goapp-deployment
  278  kubectl get all
  279  kubectl delete deployment.apps/go-app-deployment
  280  kubectl get all
  281  kubectl delete deployment.apps/go-app-deployment
  282  kubectl get all
  283  kubectl delete service/goapp-service
  284  kubectl delete service/go-app-service
  285  kubectl get all
  286  minikube status
  287  kubectl delete deployment.apps/go-app-deployment
  288  kubectl get all
  289  kubectl delete pod/go-app-deployment-58bf7c7d57-4h5nx
  290  kubectl get all
  291  kind delete cluster
  292  history
  293  kind get all
  294  kubectl get all
  295  kubectl config current-context
  296  kind delete cluster --name=kind-3-node-kind-cluster
  297  kubectl get all
  298  history
mir@DESKTOP-JASRD4A:~$ 
```
