```
    1  lsb_release -a
    2  ls
    3  cd ..
    4  ls
    5  mkdir go-learn
    6  cd go-learn/
    7  code .
    8  exit
    9  git -version
   10  git --version
   11  git remote -v
   12  git status
   13  git init
   14  git remote -v
   15  ls
   16  git remote add origin https://github.com/mir-owahed/go-lang-app.git
   17  git remote -v
   18  git status
   19  git add .
   20  git status
   21  git commit -m "go language hello app and dockerfile added"
   22  ssh-keygen
   23  ls
   24  ls -la
   25  cat /home/codespace/.ssh/id_rsa.pub
   26  git config --global user.name "Mir Ali"
   27  git config --global user.email bachchu333@gmail.com
   28  git push -u origin main
   29  git remote -v
   30  git remote add origin https://github.com/mir-owahed/go-lang-app.git
   31  git remote -v
   32  git branch -M main
   33  git push -u origin main
   34  git config credential.helper store
   35  git push -u origin main
   36  git push
   37  git push --set-upstream origin main
   38  git push
   39  git push --set-upstream origin main
   40  git status
   41  git remote add origin https://github.com/mir-owahed/go-lang-app.git
   42  git push --set-upstream origin main
   43  git push
   44  git push --set-upstream origin main
   45  git push -u origin main
   46  exit
   47  ls -la 
   48  ls -la /
   49  ls -la ~/home
   50  kubectl version --client
   51  kubectl get nodes 
   52  docker ps
   53  docker ps -a
   54  kubectl get namespaces 
   55  kubectl get nodes 
   56  kubectl get nodes -o wide
   57  kubectl config get-clusters 
   58  kubectl config current-context 
   59  kubectl get all
   60  ls
   61  kubectl apply -f k8s-deployment.yaml 
   62  kubectl get pod
   63  kubectl get pod -o wide
   64  kubectl get pod --watch
   65  kubectl get deployments.apps 
   66  kubectl apply -f k8s-service.yaml 
   67  kubectl get svc
   68  curl http:localhost:3000
   69  apt install curl
   70  sudo apt install curl
   71  curl http://localhost:3000
   72  curl http://localhost:3007
   73  kubectl get pod
   74  kubectl describe pod go-deployment-7c98b5f775-799w7
   75  curl 10.240.0.3:3007
   76  curl 10.240.0.3:3000
   77  curl 10.244.0.3:3000
   78  curl 10.244.0.3:3007
   79  curl 192.168.49.2:3007
   80  curl http://192.168.49.2:3007
   81  curl http://192.168.49.2:3000
   82  curl http://192.168.49.2:8000
   83  curl http://192.168.49.2:30007
   84  curl http://192.168.49.2:30007/ping
   85  curl http://192.168.49.2:30007/hello
   86  curl http://10.244.0.3:30007/hello
   87  kubectl get svc
   88  curl http://10.107.80.5:30007/hello
   89  kubectl get deployments.apps 
   90  kubectl describe deployments.apps 
   91  kubectl get pod
   92  kubectl describe pod go-deployment-7c98b5f775-9r87j
   93  git status
   94  git remote -v
   95  git add .
   96  git commit -m "k8s deployment and service yaml added"
   97  git push
   98  docker images
   99  kubectl get all
  100  kubectl delete deployments.apps 
  101  kubectl delete deployments.apps deployment.apps/go-deployment
  102  kubectl delete deployment deployment.apps/go-deployment
  103  kubectl delete deployment go-deployment 
  104  kubectl get pods
  105  kubectl get all
  106  kubectl delete svc go-service 
  107  kubectl get all
  108  minikube status
  109  minikube stop
  110  docker ps
  111  docker ps -a
  112  docker images
  113  docker rmi my-golang-app
  114  docker rmi my-golang-app:latest
  115  docker rmi 7f842a766deb
  116  docker images
  117  kubectl get nodes
  118  exit
  119  docker images
  120  docker ps
  121  docker ps -a
  122  docker rm 1c4e2a0715aa
  123  docker ps -a
  124  history
  125  docker build -t goapi:0.0.1 .
  126  docker images
  127  docker run --rm -p 3000:8000 goapi:0.0.1
  128  docker ps -a
  129  sudo su
  130  docker ps -a
  131  docker rm 831fdbd43d82
  132  docket stop 831fdbd43d82
  133  docker stop 831fdbd43d82
  134  docker ps
  135  docker run --rm -p 8000:8000 goapi:0.0.1
  136  history
  137  clear
  138  docker run -d -p 3000:8000 goapi:0.0.1
  139  docker ps
  140  docker logs eba9c43ea9fa
  141  curl http://localhost:3000
  142  curl http://localhost:3000/hello
  143  curl http://localhost:3000/ping
  144  docker logs eba9c43ea9fa
  145  docker inspect eba9c43ea9fa
  146  docker inspect eba9c43ea9fa | vim -
  147  docker --help
  148  docker describe --help
  149  clear 
  150  docker exec -it eba9c43ea9fa /bin/bash
  151  docker images
  152  docker ps
  153  docker stop eba9c43ea9fa
  154  docker ps
  155  docker ps -a
  156  docker stop eba9c43ea9fa
  157  docker ps -a
  158  docker rm eba9c43ea9fa
  159  docker ps -a
  160  history
```
