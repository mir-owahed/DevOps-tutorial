```
ubuntu@ip-10-0-0-245:~$ history
    1  sudo apt update
    2  sudo apt  install -y docker.io
    3  sudo chmod 666 /var/run/docker.sock
    4  sudo apt-get install -y wget apt-transport-https gnupg lsb-release
    5  sudo apt-get install -y apt-transport-https ca-certificates curl gpg
    6  sudo mkdir -p -m 755 /etc/apt/keyrings
    7  curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    8  echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
    9  sudo apt-get -y update
   10  sudo apt install kubeadm=1.30.0-1.1 kubectl=1.30.0-1.1 kubelet=1.30.0-1.1 -y
   11  sudo kubeadm init --pod-network-cidr=10.244.0.0/16
   12  kubectl get nodes
   13  mkdir -p $HOME/.kube
   14  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   15  sudo chown $(id -u):$(id -g) $HOME/.kube/config
   16  kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/calico.yaml
   17  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
   18  kubectl get nodes
   19  ls
   20  ls -la
   21  cd .kube/
   22  ls
   23  cd
   24  kubectl create namespace argocd
   25  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   26  kubectl get pods -n argocd
   27  kubectl get all -n argocd
   28  kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
   29  kubectl get all -n argocd
   30  history
ubuntu@ip-10-0-0-245:~$
```
