KinD kubernetes command
```
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
mir@DESKTOP-JASRD4A:~$
```
