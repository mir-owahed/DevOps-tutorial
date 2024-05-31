# Getting started with terraform aws on ubuntu

## pre-requisite
- terraform cli
- aws cli
- aws configure

```
cd /opt/

sudo mv ~/Downloads/terraform_1.8.4_linux_amd64.zip /opt/

sudo unzip terraform_1.8.4_linux_amd64.zip 
sudo chmod +x terraform

./terraform 

cd

terraform

export PATH=$PATH:/opt/

cd

terraform

pip install awscli
[curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install]

aws

aws --version
[Create IAM user and create access key and secret access key]
aws configure
```
## terraform commands
```
terraform --help
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform destroy
terraform show
```

Reference [Download binaries](https://developer.hashicorp.com/terraform/install?product_intent=terraform#linux).

[AWS Reference](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

