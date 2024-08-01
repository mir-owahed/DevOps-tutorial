```
### install self-hosted k8s on vm
    1  sudo apt update
    2  nano install.sh
    3  ls
    4  sudo chmod +x install.sh
    5  ls
    6  ./install.sh
    7  sudo kubeadm init --pod-network-cidr=10.244.0.0/16
    8  mkdir -p $HOME/.kube
    9  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   10  sudo chown $(id -u):$(id -g) $HOME/.kube/config
   11  kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/calico.yaml
   12  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
   13  kubectl get nodes
```
