## Install kubernetes on vm , prefer t3.medium, 25gb storage
## Step1:
```markdown




### On control plane and worker node

sudo apt  install -y docker.io
sudo chmod 666 /var/run/docker.sock
sudo apt-get install wget apt-transport-https gnupg lsb-release
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt install kubeadm=1.30.0-1.1 kubectl=1.30.0-1.1 kubelet=1.30.0-1.1 -y

```

## Step2:

### On control plane:

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```
It generates token . Run the command on worker node with sudo
## Step3:

### On control plane:

```bash
mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## Step4:

### On control plane:

```bash
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/calico.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
```
## Step5:
Open the following port
```
smtp 25
custom tcp 3000-10000
http 80
https 443
custom tcp 587
ssh 22
custom tcp 6443
custom tcp 30000-32767
smtp 465
custom tcp 27017
```
```
On control plane
6443/tcp for Kubernetes API Server
2379-2380 for etcd server client API
6783/tcp,6784/udp for Weavenet CNI
10248-10260 for Kubelet API, Kube-scheduler, Kube-controller-manager, Read-Only Kubelet API, Kubelet health
80,8080,443 Generic Ports
30000-32767 for NodePort Services
```
```
On worker node
6783/tcp,6784/udp for Weavenet CNI
10248-10260 for Kubelet API etc
30000-32767 for NodePort Services
```
References:
1. <https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/>
2. <https://kubernetes.io/docs/reference/networking/ports-and-protocols/>
