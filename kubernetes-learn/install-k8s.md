![components-of-kubernetes](https://github.com/user-attachments/assets/4debe92f-b903-4aa0-8c50-bfec8b77c67e)
## Install self-hosted multinode kubernetes cluster using kubeadm on vm

```
Prerequisite:
prefer t2.medium, 25gb storage, 2 vm (1 for control-plane and 1 for worker-node)
```
## Step1:
```
### On control-plane and worker-node
sudo apt update
sudo apt  install -y docker.io
sudo chmod 666 /var/run/docker.sock
sudo apt-get install -y wget apt-transport-https gnupg lsb-release
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get -y update
sudo apt install kubeadm=1.30.0-1.1 kubectl=1.30.0-1.1 kubelet=1.30.0-1.1 -y

```

## Step2:

### On control-plane:

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```
It generates token . Run the command on worker node with sudo
## Step3:

### On control-plane:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## Step4:

### On control-plane:

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
On control-plane
6443/tcp for Kubernetes API Server
2379-2380 for etcd server client API
6783/tcp,6784/udp for Weavenet CNI
10248-10260 for Kubelet API, Kube-scheduler, Kube-controller-manager, Read-Only Kubelet API, Kubelet health
80,8080,443 Generic Ports
30000-32767 for NodePort Services
```
```
On worker-node
6783/tcp,6784/udp for Weavenet CNI
10248-10260 for Kubelet API etc
30000-32767 for NodePort Services
```
### Install kubectl on linux vm and connect k8s cluster configuring kubeconfig
```
curl -LO "<https://dl.k8s.io/release/$>(curl -L -s <https://dl.k8s.io/release/stable.txt>)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
[mkdir -p ~/.local/bin]
sudo mv ./kubectl ~/.local/bin/kubectl
nano kubeconfig.yaml
past it
export KUBECONFIG=kubeconfig.yaml
kubectl get nodes
kubectl cluster-info
```
install kubectl
```
ubuntu@ip-10-0-0-199:~$ history
    1  sudo apt update
    2  chmod +x kubectl
    3  sudo chmod +x kubectl
    4  ls
    5  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    6  sudo chmod +x kubectl
    7  ls
    8  mkdir -p ~/.local/bin
    9  ls
   10  mv ./kubectl ~/.local/bin/kubectl
   11  ls
   12  kubectl version --client
   13  nano kubeconfig.yaml
   14  export KUBECONFIG=kubeconfig.yaml
   15  kubectl get nodes
   16  cd ~/.local/bin/kubectl
   17  cd ~/.local/bin/
   18  ls
   19  nano kubeconfig.yaml
   20  export KUBECONFIG=kubeconfig.yaml
   21  kubectl get nodes
   22  sudo apt-get install -y kubectl
   23  cd
   24  sudo apt-get install -y kubectl
   25  hello
   26  sudo apt update
   27  sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
   28  curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
   29  sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring
   30  echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
   31  sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   # helps tools such as command-not-found to work correctly
   32  sudo apt-get update
   33  sudo apt-get install -y kubectl
   34  kubectl cluster-info
   35  kubectl get nodes
   36  history
ubuntu@ip-10-0-0-199:~$
```

References:
1. <https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/>
2. <https://kubernetes.io/docs/reference/networking/ports-and-protocols/>
3. <https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-on-linux>
