![eks](https://github.com/user-attachments/assets/f427e4a8-83eb-4f78-addd-566220053dd7)
create secure eks cluster using aws console
  - Create vpc containing 2 public subnet in 2 az and private subnet in 2 az
  - Igw and Nat gw
.....................................
- EKS >> add cluster (configure control plane)

- IAM >> Role >> EKS cluster role >> choose eks cluster >> 

- Choose networking >> vpc and private subnet>> SG -NO >> Cluster endpoint Private

............................
- add node group
- Create IAM role for node group >> IAM > role> aws service > ec2> permission > worker node policy, container registry read only, eks cni policy>create
- network > subnet > private
- configure remote access > choose key pair > choose SG
```
aws configure
aws sts get-caller-identity
kubectl config view
kubectl cluster-info
kubectl get nodes
```
