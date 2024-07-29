## Install kubernetes on vm , prefer t3.medium, 25gb storage
## Step1:
```markdown




### On control plane and worker node


sudo apt  install -y docker.io
sudo chmod 666 /var/run/docker.sock
sudo apt-get install wget apt-transport-https gnupg lsb-release
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
sudo mkdir -p -m 755 /etc/apt/keyrings
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list
apt-get update
apt install kubeadm=1.30.0-1.1 kubectl=1.30.0-1.1 kubelet=1.30.0-1.1 -y
```

## Step2:

### On control plane:

```bash
kubeadm init --pod-network-cidr=192.168.0.0/16
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

