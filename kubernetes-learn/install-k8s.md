## --- KUBERNETES Install Steps ---
```markdown


## Step1:

### On Master and slave


apt-get update -y
apt-get install docker.io -y
service docker restart
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list
apt-get update
apt install kubeadm=1.30.0-1.1 kubectl=1.30.0-1.1 kubelet=1.30.0-1.1 -y
```

## Step2:

### On Master node:

```bash
kubeadm init --pod-network-cidr=192.168.0.0/16
```

## Step3:

### On Master node:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## Step4:

### On Master node:

```bash
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.1/manifests/calico.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
```