```
mir@ubuntu22-VBox:~/Documents/k8s-learn/go-lang-app$ cd ~/.kube/

mir@ubuntu22-VBox:~/.kube$ ls

cache  config

mir@ubuntu22-VBox:~/.kube$ vim config 

mir@ubuntu22-VBox:~/.kube$ kubectl config current-context

minikube

mir@ubuntu22-VBox:~/.kube$ kubectl cluster-info

Kubernetes control plane is running at https://192.168.76.2:8443

CoreDNS is running at https://192.168.76.2:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy



To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

mir@ubuntu22-VBox:~/.kube$ kubectl config get-clusters

NAME

minikube

mir@ubuntu22-VBox:~/.kube$ kubectl get nodes

NAME       STATUS   ROLES           AGE     VERSION

minikube   Ready    control-plane   2d20h   v1.30.0

mir@ubuntu22-VBox:~/.kube$ kubectl get namespace

NAME              STATUS   AGE

default           Active   2d21h

kube-node-lease   Active   2d21h

kube-public       Active   2d21h

kube-system       Active   2d21h

mir@ubuntu22-VBox:~/.kube$ kubectl config view | grep namespace

    namespace: default

mir@ubuntu22-VBox:~/.kube$ minikube daskboard

Error: unknown command "daskboard" for "minikube"



Did you mean this?

	dashboard



Run 'minikube --help' for usage.

mir@ubuntu22-VBox:~/.kube$ minikube dashboard

🔌  Enabling dashboard ...

    ▪ Using image docker.io/kubernetesui/dashboard:v2.7.0

    ▪ Using image docker.io/kubernetesui/metrics-scraper:v1.0.8

💡  Some dashboard features require the metrics-server addon. To enable all features please run:



	minikube addons enable metrics-server



🤔  Verifying dashboard health ...

🚀  Launching proxy ...

🤔  Verifying proxy health ...

^C

mir@ubuntu22-VBox:~/.kube$ minikube addons enable metrics-server

💡  metrics-server is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.

You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS

    ▪ Using image registry.k8s.io/metrics-server/metrics-server:v0.7.1

🌟  The 'metrics-server' addon is enabled

mir@ubuntu22-VBox:~/.kube$ minikube dashboard

🤔  Verifying dashboard health ...

🚀  Launching proxy ...

🤔  Verifying proxy health ...

🎉  Opening http://127.0.0.1:34615/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...

ln: failed to create symbolic link '/run/user/1000/snap.firefox/wayland-0': File exists

Gtk-Message: 14:19:46.455: Not loading module "atk-bridge": The functionality is provided by GTK natively. Please try to not load it.

[GFX1-]: ManageChildProcess(glxtest): poll failed: Success



[GFX1-]: glxtest: ManageChildProcess failed



[GFX1-]: No GPUs detected via PCI



^C

mir@ubuntu22-VBox:~/.kube$ docker images

REPOSITORY                    TAG       IMAGE ID       CREATED       SIZE

owahed1/go-lang-app           0.0.2     ce2b26da9017   2 hours ago   303MB

go-lang-app                   multi     747a9abaccaf   5 days ago    303MB

go-lang-app                   0.0.1     20541ffddfa7   6 days ago    310MB

owahed1/go-lang-app           0.0.1     20541ffddfa7   6 days ago    310MB

gcr.io/k8s-minikube/kicbase   v0.0.44   5a6e59a9bdc0   11 days ago   1.26GB

mir@ubuntu22-VBox:~/.kube$ docker login

Authenticating with existing credentials...

WARNING! Your password will be stored unencrypted in /home/mir/.docker/config.json.

Configure a credential helper to remove this warning. See

https://docs.docker.com/engine/reference/commandline/login/#credentials-store



Login Succeeded

mir@ubuntu22-VBox:~/.kube$ docker push owahed1/go-lang-app:0.0.2

The push refers to repository [docker.io/owahed1/go-lang-app]

8f84224dc652: Pushed 

cf5c5acd4e69: Pushed 

7796592df80a: Pushed 

5f70bf18a086: Layer already exists 

05ca67b828bd: Mounted from library/golang 

34262b42df70: Mounted from library/golang 

d542c684019d: Mounted from library/golang 

d4fc045c9e3a: Layer already exists 

0.0.2: digest: sha256:60fd8bf7c535868a780235fda331c4eb576de7dff03d875a3b86773b27ac09ee size: 1990

mir@ubuntu22-VBox:~/.kube$ docker tag --help



Usage:  docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]



Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE



Aliases:

  docker image tag, docker tag

mir@ubuntu22-VBox:~/.kube$ # smallest unit of computing in k8s is a Pod

mir@ubuntu22-VBox:~/.kube$ cd

mir@ubuntu22-VBox:~$ cd Do

Documents/ Downloads/ 

mir@ubuntu22-VBox:~$ cd Documents/k8s-learn/

mir@ubuntu22-VBox:~/Documents/k8s-learn$ vim golang-deployment.yaml

mir@ubuntu22-VBox:~/Documents/k8s-learn$ ls

go-lang-app  golang-deployment.yaml

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl apply -f go

go-lang-app/            golang-deployment.yaml  

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl apply -f golang-deployment.yaml 

deployment.apps/go-lang-deployment created

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl get deployments

NAME                 READY   UP-TO-DATE   AVAILABLE   AGE

go-lang-deployment   0/3     3            0           17s

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl get pods 

NAME                                  READY   STATUS              RESTARTS   AGE

go-lang-deployment-76d89fd497-bmczr   0/1     ContainerCreating   0          24s

go-lang-deployment-76d89fd497-kx2v8   0/1     ContainerCreating   0          24s

go-lang-deployment-76d89fd497-vtnwf   0/1     ContainerCreating   0          24s

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl get pods --watch

NAME                                  READY   STATUS              RESTARTS   AGE

go-lang-deployment-76d89fd497-bmczr   0/1     ContainerCreating   0          33s

go-lang-deployment-76d89fd497-kx2v8   0/1     ContainerCreating   0          33s

go-lang-deployment-76d89fd497-vtnwf   0/1     ContainerCreating   0          33s

    







go-lang-deployment-76d89fd497-vtnwf   1/1     Running             0          2m23s

go-lang-deployment-76d89fd497-kx2v8   1/1     Running             0          2m27s

go-lang-deployment-76d89fd497-bmczr   1/1     Running             0          2m28s

^Cmir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl get pods

NAME                                  READY   STATUS    RESTARTS   AGE

go-lang-deployment-76d89fd497-bmczr   1/1     Running   0          3m38s

go-lang-deployment-76d89fd497-kx2v8   1/1     Running   0          3m38s

go-lang-deployment-76d89fd497-vtnwf   1/1     Running   0          3m38s

mir@ubuntu22-VBox:~/Documents/k8s-learn$ 
mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl describe --help

Show details of a specific resource or group of resources.
mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl describe pod go-lang-deployment-76d89fd497-kx2v8 | vim -

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl get deployment

NAME                 READY   UP-TO-DATE   AVAILABLE   AGE

go-lang-deployment   3/3     3            3           14m

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl  describe deployment go-lang-deployment

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl  describe deployment go-lang-deployment | vim -

Vim: Reading from stdin...



mir@ubuntu22-VBox:~/Documents/k8s-learn$ #https://kubernetes.io/docs/concepts/services-networking/service/

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl expose --help

mir@ubuntu22-VBox:~/Documents/k8s-learn$ vim goapp-service.yaml

mir@ubuntu22-VBox:~/Documents/k8s-learn$ ls

goapp-service.yaml  go-lang-app  golang-deployment.yaml

mir@ubuntu22-VBox:~/Documents/k8s-learn$ vim goapp-service.yaml 

mir@ubuntu22-VBox:~/Documents/k8s-learn$ vim goapp-service.yaml 

mir@ubuntu22-VBox:~/Documents/k8s-learn$ vim goapp-service.yaml 

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl apply -f goapp-service.yaml 

service/goapp created

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl get services

NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE

goapp        NodePort    10.110.148.161   <none>        3000:30007/TCP   8s

kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP          2d22h

mir@ubuntu22-VBox:~/Documents/k8s-learn$ curl http://localhost:30007

curl: (7) Failed to connect to localhost port 30007 after 37 ms: Connection refused

mir@ubuntu22-VBox:~/Documents/k8s-learn$ curl 10.110.148.161:30007

^C

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl get nodes

NAME       STATUS   ROLES           AGE     VERSION

minikube   Ready    control-plane   2d22h   v1.30.0

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl get pods

NAME                                  READY   STATUS    RESTARTS   AGE

go-lang-deployment-76d89fd497-bmczr   1/1     Running   0          38m

go-lang-deployment-76d89fd497-kx2v8   1/1     Running   0          38m

go-lang-deployment-76d89fd497-vtnwf   1/1     Running   0          38m

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl  describe pod go-lang-deployment-76d89fd497-kx2v8

mir@ubuntu22-VBox:~/Documents/k8s-learn$ kubectl  describe pod go-lang-deployment-76d89fd497-kx2v8

Name:             go-lang-deployment-76d89fd497-kx2v8

Namespace:        default

Priority:         0

Service Account:  default

Node:             minikube/192.168.76.2

Start Time:       Mon, 20 May 2024 15:22:51 +0530

Labels:           app=goapi

                  pod-template-hash=76d89fd497

Annotations:      <none>

Status:           Running

IP:               10.244.0.8

IPs:

  IP:           10.244.0.8

Controlled By:  ReplicaSet/go-lang-deployment-76d89fd497

Containers:

  go-lang-app:

    Container ID:   docker://d12ee83e224c3393d62dba9203fdfa0d92aa684a3d64e61ef445024affd972a3

    Image:          owahed1/go-lang-app:0.0.2

    Image ID:       docker-pullable://owahed1/go-lang-app@sha256:60fd8bf7c535868a780235fda331c4eb576de7dff03d875a3b86773b27ac09ee

    Port:           8000/TCP

    Host Port:      0/TCP

    State:          Running

      Started:      Mon, 20 May 2024 15:25:15 +0530

    Ready:          True

    Restart Count:  0

    Environment:    <none>

    Mounts:

      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-h4dp4 (ro)

Conditions:

  Type                        Status

  PodReadyToStartContainers   True 

  Initialized                 True 

  Ready                       True 

  ContainersReady             True 

  PodScheduled                True 

Volumes:

  kube-api-access-h4dp4:

    Type:                    Projected (a volume that contains injected data from multiple sources)

    TokenExpirationSeconds:  3607

    ConfigMapName:           kube-root-ca.crt

    ConfigMapOptional:       <nil>

    DownwardAPI:             true

QoS Class:                   BestEffort

Node-Selectors:              <none>

Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s

                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s

Events:

  Type    Reason     Age   From               Message

  ----    ------     ----  ----               -------

  Normal  Scheduled  38m   default-scheduler  Successfully assigned default/go-lang-deployment-76d89fd497-kx2v8 to minikube

  Normal  Pulling    38m   kubelet            Pulling image "owahed1/go-lang-app:0.0.2"

  Normal  Pulled     36m   kubelet            Successfully pulled image "owahed1/go-lang-app:0.0.2" in 9.073s (2m3.429s including waiting). Image size: 302991957 bytes.

  Normal  Created    36m   kubelet            Created container go-lang-app

  Normal  Started    36m   kubelet            Started container go-lang-app

mir@ubuntu22-VBox:~/Documents/k8s-learn$ curl http://192.168.76.2:30007

404 page not found

mir@ubuntu22-VBox:~/Documents/k8s-learn$ curl http://192.168.76.2:30007/hello

HELLO WORLD!!mir@ubuntu22-VBox:~/Documents/k8s-learn$ curl http://192.168.76.2:30007/ping



```
