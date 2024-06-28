# EC2 as Gitlab runner and use docker executor on it

## Breif Overview 

### Create an EC2 instance:
   -  Create an EC2 instance on AWS.
   -  Install GitLab Runner on the EC2 instance.
   -  Register the runner with your GitLab instance.
   -  Install Java (openjdk-11-jre)
   -  Install Docker
   
## AWS EC2 Instance Configuration

- Go to AWS Console
- Instances(running)
- Launch instances


## Docker Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```

All the required configuration is setup !!!






