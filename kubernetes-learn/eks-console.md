# How to Create a Secured Kubernetes Cluster on AWS EKS Using AWS Console

![eks](https://github.com/user-attachments/assets/f427e4a8-83eb-4f78-addd-566220053dd7)


In this guide, you'll learn how to set up a secure Kubernetes cluster on AWS Elastic Kubernetes Service (EKS) using the AWS Management Console. We’ll configure a bastion host in the public subnet, deploy your Kubernetes cluster and node group in private subnets, and deploy a sample application to ensure everything is functioning correctly.

## Prerequisites

Before getting started, ensure you have the following:
- An **AWS account** with sufficient permissions.
- **AWS CLI** (optional, but recommended for easier cluster management).
- **kubectl** installed and configured on your local machine.

---
## Watch the Tutorial

[![Create a Private EKS Cluster on AWS Console](https://github.com/user-attachments/assets/18e81e91-97b1-41f9-be30-018d8cf2fedd)](https://youtu.be/MXvLcwbYb8E)

[Watch the full tutorial on YouTube](https://youtu.be/MXvLcwbYb8E) to follow along with step-by-step instructions.

[![Create a secured Kubernetes cluster on AWS EKS](https://img.youtube.com/vi/XWaLU0alrvY/0.jpg)](https://youtu.be/XWaLU0alrvY)

[Watch the full tutorial on YouTube](https://youtu.be/XWaLU0alrvY) to follow along with step-by-step instructions.

---
## Step 1: Create a VPC with Public and Private Subnets

To begin, you’ll need a VPC to host your cluster.

1. Navigate to the **VPC Console** in AWS.
2. Click on **Create VPC** and configure the following:
   - **VPC CIDR Block**: e.g., `10.0.0.0/16`.
   - **Subnets**: Create both public and private subnets across multiple availability zones for redundancy.
   - **Internet Gateway**: Attach this to the public subnet to allow external access.
   - **Route Tables**: Ensure you configure routing between the subnets properly, with the public subnet routing to the internet gateway.

You can use AWS-provided EKS VPC templates to automate some of this configuration.

---

## Step 2: Create a Bastion Host in the Public Subnet

To securely access your private Kubernetes cluster, you'll need a bastion host in the public subnet.

1. Go to the **EC2 Console** and click **Launch Instance**.
2. Choose an instance type, e.g., **t2.micro** for small workloads.
3. Select your **public subnet** in the **Network** section.
4. Create or select an existing key pair for SSH access.
5. Configure **Security Groups** to allow SSH access (port 22) from your IP address.
6. Launch the instance.
7. User data
```
#!/bin/bash
apt-get update -y
apt-get install -y unzip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
./aws/install
curl -LO "https://dl.k8s.io/release/v1.31.0/bin/linux/amd64/kubectl"
install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
aws --version
kubectl version --client
```
---

## Step 3: Create an IAM Role for Control Plane and Worker Nodes
create an IAM role for your Cluster
1. Go to the **IAM Console** and create a new role.
2. Choose **EKS Cluster** as the trusted entity.
3. Attach the following managed policies:
  `AmazonEKSClusterPolicy`
4. Name the role (e.g., `eks-cluster-role`) and create it.


Now we’ll create an IAM role for your worker nodes.

1. Go to the **IAM Console** and create a new role.
2. Choose **EC2** as the trusted entity.
3. Attach the following managed policies:
   - `AmazonEKSWorkerNodePolicy`
   - `AmazonEKS_CNI_Policy`
   - `AmazonEC2ContainerRegistryReadOnly`
4. Name the role (e.g., `eks-node-role`) and create it.

---
---

## Step 4: Create an EKS Cluster

1. Go to the **Amazon EKS Console** and click **Create Cluster**.
2. Fill out the following details:
   - **Cluster Name**: Give your cluster a name.
   - **Kubernetes Version**: Choose the latest stable version.
   - **Role**: Select an appropriate IAM role with the `AmazonEKSClusterPolicy` attached.
   - **VPC and Subnets**: Select the VPC and **private subnets** created earlier.
   - **Security Group**: Ensure the security group allows communication between the control plane and worker nodes.

3. Click **Create** and wait for the cluster to be provisioned.



## Step 5: Create a Node Group in the Private Subnets

1. In the **EKS Console**, select your cluster and navigate to the **Compute** tab.
2. Click **Add Node Group**.
3. Fill out the following details:
   - **Node Group Name**: Choose a name (e.g., `private-node-group`).
   - **IAM Role**: Select the IAM role you created earlier.
   - **Subnets**: Select the **private subnets** for the worker nodes.
   - **Instance Type**: Choose an instance type such as **t3.medium**.
   - **Scaling Configuration**: Set desired, minimum, and maximum nodes.
4. Click **Create** and wait for the node group to be ready.

---
## Step : Edit Security Group in the EKS Cluster

1. In the **EKS cluster**, select Networking
2. Click **Add Security Group**.
3. Fill out the following details:
   - **add 443 and bastion host sg
   - **add 33080 and bastion host sg
  
---

## Step 6: Configure kubectl to Access the Cluster

Once your cluster is running, you'll need to configure `kubectl` to interact with it.
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client

```

Once your cluster is running, you'll need to configure `aws cli` to interact with it.
```
sudo apt update -y
sudo apt install unzip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version

```
aws configure
```
aws configure
```
1. Open your terminal and run the following command:
   ```bash
   aws eks --region <region-code> update-kubeconfig --name <cluster-name>
   ```

2. Now, you can verify the configuration:
   ```bash
   aws eks describe-cluster --name <cluster-name>
   kubectl get nodes
   kubectl cluster-info
   ```



      Create a Kubernetes secret command
```
kubectl create secret docker-registry ecr-credentials \  
  --docker-server=<ECR-URL> \  
  --docker-username=AWS \  
  --docker-password=$(aws ecr get-login-password) \  
  --docker-email=<your-email>```
kubectl get secret
```

---

## Step 7: Deploy a Sample Application

Now that your Kubernetes cluster is set up, you can deploy a sample application.

1. Create a file named `sample-app.yaml` with the following content:
```
   
apiVersion: apps/v1
kind: Deployment # Kubernetes resource kind we are creating
metadata:
  name: goapp-deployment
spec:
  selector:
    matchLabels:
      app: goapp
  replicas: 2 # Number of replicas that will be created for this deployment
  template:
    metadata:
      labels:
        app: goapp
    spec:
      containers:
        - name: goapp
          image: owahed1/go-lang-app:0.0.2 # Image that will be used to containers in the cluster
          imagePullPolicy: Always
          ports:
            - containerPort: 8000 # The port that the container is running on in the cluster


---

apiVersion: v1 # Kubernetes API version
kind: Service # Kubernetes resource kind we are creating
metadata: # Metadata of the resource kind we are creating
  name: goapp-service
spec:
  selector:
    app: goapp
  ports:
    - protocol: "TCP"
      port: 80
      targetPort: 8000 
  type: LoadBalancer # type of the service.

```
2. Deploy the application with:
   ```bash
   kubectl apply -f sample-app.yaml
   ```

3. Check if the application is running:
   ```bash
   kubectl get pods
   ```

4. The application will create an external LoadBalancer, which you can access to test your deployment.

---

## Step 8: Access the Application 

---
## Delete eks cluster
```
delete node group first
delete cluster
delete NAT Gateway
delete VPC
delete Load Balancer
delete elastic IP
```
