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

aws

aws --version

aws configure
```

Reference [Download binaries](https://developer.hashicorp.com/terraform/install?product_intent=terraform#linux).
