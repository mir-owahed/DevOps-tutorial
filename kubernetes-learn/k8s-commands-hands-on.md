# kubernetes commands practice
```
 killercoda practice
	 19  docker ps
   20  k get nodes
   21  kubectl --help
   22  k apply --help
   23  kubectl --help
   24  kubectl version
   25  k get nodes
   26  ls
   27  cd
   28  ls
   29  ls -la
   30  cd .kube/
   31  ls
   32  pwd
   33  ls -la
   34  vim config 
   35  kubectl config current-context 
   36  kubectl cluster-info 
   37  k config get-clusters 
   38  k get nodes
   39  #namespace
   40  k get namespaces 
   41  k config view | grep namespace
   42  kubectl config view | grep namespace
   43  docker images
   44  kubectl create deployment goapp --image=owahed1/k8s-hello-go:latest
   45  k get deployments
   46  k get pods --watch
   47  k get pods
   48  k describe --help
   49  k get pods
   50  k describe pod goapp-7d5f7c6f9-ldc9h
```

# more commands
```
   14  docker ps
   15  k get pod
   16  nano service.yaml
   17  k apply -f service.yaml 
   18  k get pod
   19  k get all
   20  k get svc
   21  ls
   22  nano service.yaml 
   23  ssh node01 
   24  k get svc
   25  ssh node01 
   26  nano service.yaml 
   27  k get svc
   28  ssh node01 
   29  nano service.yaml 
   30  ssh node01 
   31  k get pod
   32  k describe pod goapp-7c6fcbd469-5j6qt
   33  exit
   34  k get deployments
   35  k get pods
   36  k describe pod goapp-7c6fcbd469-5j6qt
   37  exit
   38  k get nodes 
   39  k get all
   40  k delete deployments.apps 
   41  k get deployments.apps 
   42  k get deployments
   43  k delete deployments goapp 
   44  k get deployments
   45  k get pod
   46  k get all
   47  k delete svc goapp 
   48  k get all
```
# more
```
 k get nodes
    5  ls
    6  k get deploy
    7  k get deployments.apps 
    8  k get service
    9  vim deployment.yaml
   10  k get deployments.apps 
   11  nano deployment.yaml 
   12  k apply -f deployment.yaml 
   13  k get deployments
   14  k get deployments -o wide
   15  k get pods
   16  k get pods -o wide
   17  k get nodes
   18  k get pods
   19  k get deployments.apps 
   20  k get deployments -o wide
   21  k get pods -o wide
   22  k describe pod hellogo-deployment-5cb6964685-jpfwn
   23  k get all
   24  k describe pod pod/hellogo-deployment-5cb6964685-jqr7f
   25  k describe pod/hellogo-deployment-5cb6964685-jqr7f
   26  clear
   27  k get all
   28  k get nodes -o wide
   29  k get pods -o wide
   30  k describe hellogo-deployment-5cb6964685-jqr7f
   31  k describe pod hellogo-deployment-5cb6964685-jqr7f
   32  clear
   33  k get pod
   34  k get pods -o wide
   35  k describe pod hellogo-deployment-5cb6964685-jpfwn
   36  kk
   37  k clear
   38  clear
   39  k get all -o wide
   40  ls
   41  vim service.yaml
   42  ls
   43  ll
   44  l
   45  k apply -f service.yaml 
   46  k get svc
   47  k get all
   48  ls
   49  nano service.yaml 
   50  ip a
   51  nano service.yaml 
   52  k apply -f service.yaml 
   53  k get all
   54  k get all -o wide
   55  k get all
   56  curl -L http://192.168.1.4:30007/hello
   57  curl -L http://10.105.159.104:30007/hello
   58  curl http://10.105.159.104:30007/hello
   59  kubectl cluster-info
   60  k get namespaces
   61  docker images
   62  docker ps
   63  k images
   64  k get images
   65  k get nodes all
   66  k get all
   67  k get nodes
   68  k get nodes -o wide
   69  kubectl cluster-info
   70  ssh node01
```
