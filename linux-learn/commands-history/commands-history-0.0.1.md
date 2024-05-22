```
    1  sudo apt install nano
    2  su -
    3  sudo apt install nano
    4  history
    5  sudo visudo
    6  sudo vim install_docker.sh
    7  sudo apt install vim
    8  sudo vim install_docker.sh
    9  sudo chmod +x install_docker.sh 
   10  ./install_docker.sh 
   11  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   12  sudo groupadd docker
   13  sudo usermod -aG docker $USER
   14  docker --version
   15  docker -version
   16  docker version
   17  docker compose version
   18  docker compose --version
   19  ls
   20  ls -la
   21  top
   22  apt install git
   23  sudo apt install git
   24  git --version
   25  git clone https://github.com/mir-owahed/SRE101.git
   26  ls
   27  cd SRE101/
   28  ls
   29  cd docker-course/
   30  ls
   31  cd lesson-
   32  cd lesson-5
   33  ls
   34  cd application/
   35  ls
   36  ls -la
   37  vim app.py 
   38  vim requirements.txt 
   39  python3 --version
   40  python3 app.py 
   41  python3 install requirements.txt 
   42  sudo python3 install requirements.txt 
   43  pip install requirements.txt 
   44  sudo apt install python3-pip
   45  sudo apt update
   46  pip install requirements.txt 
   47  sudo usermod -aG docker $USER
   48  docker version
   49  newgrp docker
   50  ls 
   51  cd SRE101/docker-course/lesson-5/application/
   52  ls
   53  python app.py 
   54  python3 app.py 
   55  pin install requirements.txt 
   56  pip install requirements.txt 
   57  pip install flask
   58  python3 app.py 
   59  pip install -r requirements.txt
   60  ls
   61  vim requirements.txt 
   62  python3 app.py 
   63  pip --version
   64  vim Dockerfile
   65  docker images
   66  curl localhost:8080
   67  docker ps
   68  docker run -d -p 8080:5000 owahed1/python-sample-app
   69  docker images
   70  docker ps
   71  docker inspect a0cd63417b2e | vim -
   72  docker logs a0cd63417b2e
   73  docker logs -f a0cd63417b2e
   74  docker exec help
   75  docker exec --help
   76  docker exec a0cd63417b2e pwd
   77  docker exec a0cd63417b2e ls -la
   78  docker exec -it a0cd63417b2e bash
   79  docker ps 
   80  docker images
   81  docker rmi 435ac9a35e5f
   82  docker images
   83  docker stop 435ac9a35e5f
   84  docker stop a0cd63417b2e
   85  docker rmi 435ac9a35e5f
   86  docker images
   87  docker rm a0cd63417b2e
   88  docker images
   89  docker rmi 435ac9a35e5f
   90  docker ps -a
   91  history
   92  curl http://localhost:8000/ping
   93  history
   94  docker build -t go-lang-app:0.0.1 .
   95  ls
   96  history >> commands.txt 
   97  docker images
   98  docker run --rm -d -p 8000:8000 go-lang-app-lang-app:0.0.1 
   99  docker run --rm -d -p 8000:8000 go-lang-app:0.0.1 
  100  curl http://localhost:8000/hello
  101  curl http://localhost:8000/ping
  102  history >> commands.txt 
  103  git status
  104  git add .
  105  docker images
  106  docker tag go-lang-app:0.0.1 owahed1/go-lang-app:0.0.1
  107  docker images
  108  docker login
  109  docker push owahed1/go-lang-app:0.0.1
  110  history >> commands.txt 
  111  git status
  112  git add .
  113  git commit -m "dockerfile added"
  114  git push
  115  go run .
  116  go version
  117  export PATH=$PATH:/usr/local/go/bin
  118  go version
  119  go run .
  120  history
  121  go build 
  122  ls
  123  ls -la
  124  rm go-lang-app 
  125  git status
  126  go version
  127  go -version
  128  export PATH=$PATH:/usr/local/go/bin
  129  go -version
  130  go version
  131  go mod init github.com/mir-owahed/go-lang-app
  132  go run hello.go 
  133  go run .
  134  go build 
  135  go run .
  136  go build 
  137  git status
  138  git init
  139  git status
  140  git add .
  141  git commit -m "go lang hello app"
  142  git config --global user.name "Mir Ali"
  143  git config --global user.email bachchu333@gmail.com
  144  git remote -v
  145  git remote add origin https://github.com/mir-owahed/go-lang-app.git
  146  git remote -v
  147  git push -u origin main
  148  git push
  149  git branch -M main
  150  git push
  151  git push --set-upstream origin main
  152  history
  153  history > commands.txt
  154  git add commands.txt 
  155  git commit -m "commands.txt added"
  156  git push
  157  git log
  158  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  159  sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
  160  minikube start
  161  minikube status
  162  docker ps 
  163  docker ps
  164  docker --help
  165  docker logs --help
  166  docker ps -a
  167  docker ps
  168  docker stop aeff9ca7f94d
  169  docker ps -a
  170  docker rm aeff9ca7f94d
  171  docker ps -a
  172  docker images
  173  docker rm de883d24fc74
  174  docker ps -a
  175  docker ps
  176  docker ps --help
  177  docker run --help
  178  docker --help
  179  docker images
  180  docker rmi owahed1/python-sample-app:latest 
  181  docker images
  182  docker volume
  183  docker volume ls
  184  docker volume prune --help
  185  git --version
  186  git -V
  187  git --help
  188  clear
  189  minikube status
  190  minikube start
  191  kubectl --help
  192  kubectl --version
  193  ls
  194  kubectl version --client
  195  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  196  lls
  197  ls
  198  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
  199  echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
  200  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
  201  kubectl version --client
  202  clear
  203  #https://kubernetes.io/docs/reference/kubectl/quick-reference/
  204  docker ps
  205  clear
  206  history > commands.txt
  207  nano commands.txt 
  208  kubectl --help
  209  #kubectl <command> --help
  210  kubectl apply --help
  211  kubectl cluster-info
  212  cd Documents/
  213  ls
  214  mkdir k8s-learn
  215  cd k8s-learn/
  216  git clone https://github.com/mir-owahed/go-lang-app.git
  217  cd go-lang-app/
  218  ls
  219  docker images
  220  docker build -t owahed1/go-lang-app:0.0.2 .
  221  docker images
  222  docker run -d -p 3000:8000 owahed1/go-lang-app:0.0.2
  223  curl http://localhost:3000
  224  curl http://localhost:3000/hello
  225  curl http://localhost:3000/ping
  226  history 
  227  clear
  228  docker ps
  229  docker ps -a
  230  docker stop a755584b859a
  231  docker rm a755584b859a
  232  docker ps
  233  clear
  234  cd ~/.kube/
  235  ls
  236  vim config 
  237  kubectl config current-context
  238  kubectl cluster-info
  239  kubectl config get-clusters
  240  kubectl get nodes
  241  kubectl get namespace
  242  kubectl config view | grep namespace
  243  minikube daskboard
  244  minikube dashboard
  245  minikube addons enable metrics-server
  246  minikube dashboard
  247  docker images
  248  docker login
  249  docker push owahed1/go-lang-app:0.0.2
  250  docker tag --help
  251  # smallest unit of computing in k8s is a Pod
  252  cd
  253  cd Documents/k8s-learn/
  254  vim golang-deployment.yaml
  255  ls
  256  kubectl apply -f golang-deployment.yaml 
  257  kubectl get deployments
  258  kubectl get pods 
  259  kubectl get pods --watch
  260  kubectl get pods
  261  kubectl describe --help
  262  kubectl get pods
  263  kubectl describe go-lang-deployment-76d89fd497-kx2v8
  264  kubectl describe pod go-lang-deployment-76d89fd497-kx2v8 | vim -
  265  kubectl get deployment
  266  kubectl  describe deployment go-lang-deployment
  267  kubectl  describe deployment go-lang-deployment | vim -
  268  #https://kubernetes.io/docs/concepts/services-networking/service/
  269  kubectl expose --help
  270  vim goapp-service.yaml
  271  ls
  272  vim goapp-service.yaml 
  273  kubectl apply -f goapp-service.yaml 
  274  kubectl get services
  275  curl http://localhost:30007
  276  curl 10.110.148.161:30007
  277  kubectl get nodes
  278  kubectl get pods
  279  kubectl  describe pod go-lang-deployment-76d89fd497-kx2v8
  280  curl http://192.168.76.2:30007
  281  curl http://192.168.76.2:30007/hello
  282  curl http://192.168.76.2:30007/ping
  283  kubectl logs --help
  284  kubectl get pods
  285  kubectl logs go-lang-deployment-76d89fd497-kx2v8
  286  kubectl get all
  287  kubectl delete deployment go-lang-deployment
  288  kubectl get pods
  289  kubectl get deployments
  290  kubectl get all 
  291  kubectl delete service goapp
  292  kubectl get all
  293  minikube status
  294  minikube stop
  295  minikube delete
  296  docker ps
  297  docker ps -a
  298  exit
  299  ls
  300  cd Documents/
  301  ls
  302  cd DevOps-tutorial/
  303  ls
  304  cd ..
  305  ls
  306  rm -rf DevOps-tutorial/
  307  ls
  308  git -version
  309  git --version
  310  git clone https://github.com/mir-owahed/DevOps-tutorial.git
  311  cd DevOps-tutorial/
  312  ls
  313  cd linux-learn/
  314  ls
  315  cd commands-history/
  316  histpry
  317  history
  318  history > commands-history-0.0.1.md
```
