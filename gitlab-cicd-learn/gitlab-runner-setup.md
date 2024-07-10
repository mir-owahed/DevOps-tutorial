# EC2 as Gitlab Runner and use docker executor on CICD pipeline.

## Breif Overview 

### Create an EC2 instance:
   -  Create an EC2 instance on AWS.
   -  Install GitLab Runner on the EC2 instance.
   -  Register the runner with your GitLab instance.
   -  Install Docker
   
## AWS EC2 Instance Configuration

- Go to AWS Console
- Instances(running)
- Launch instances


## Setting up an EC2 instance as a GitLab Runner involves a few steps. Here's a detailed guide to help you through the process:
1. Launch an EC2 Instance

    Log in to AWS Management Console:
        Go to the EC2 Dashboard.
    Launch a new EC2 instance:
        Choose an Amazon Machine Image (AMI) (e.g., Amazon Linux 2 or Ubuntu).
        Select an instance type (e.g., t2.micro).
        Configure instance details (e.g., default VPC and subnet).
        Add storage (e.g., 8 GB or more).
        Add tags (optional).
        Configure security group (allow SSH access, and optionally HTTP/HTTPS if your runner will be serving web content).
    Launch the instance and download the key pair (.pem file) to SSH into your instance.

2. Install GitLab Runner on the EC2 Instance

    SSH into the EC2 instance:

```
ssh -i path/to/your-key.pem ec2-user@your-ec2-public-dns
```
## Docker Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
sudo service docker start
sudo usermod -aG docker ec2-user

```
Install GitLab Runner:
- For Ubuntu:

```
  # Download the binary for your system
sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64

# Give it permission to execute
sudo chmod +x /usr/local/bin/gitlab-runner

# Create a GitLab Runner user
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

# Install and run as a service
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
sudo gitlab-runner start
```
Command to register runner
```
sudo gitlab-runner register --url https://gitlab.com/ --registration-token GR1348941MFoBvmK3LJZdzBmqJbmy
```
    Provide the following information:

    - URL of your GitLab instance: (e.g., https://gitlab.com or your self-hosted GitLab URL)
    - Registration token: (You can find this in your GitLab project under Settings > CI/CD > Runners > Set up a specific Runner manually)
    - Description: (e.g., my-ec2-docker-runner)
    - Tags: (optional, e.g., docker,aws,ec2)
    - Executor: docker
    - Docker image: maven:3.8.4-openjdk-11

4. Configure GitLab Runner (Optional)

    Edit the config file if needed:

```
sudo nano /etc/gitlab-runner/config.toml
```
Add Docker-specific configurations:

```

    [[runners]]
      name = "my-ec2-docker-runner"
      url = "https://gitlab.com/"
      token = "YOUR_REGISTRATION_TOKEN"
      executor = "docker"
      [runners.custom_build_dir]
      [runners.docker]
        tls_verify = false
        image = "alpine:latest"
        privileged = true
        disable_entrypoint_overwrite = false
        oom_kill_disable = false
        disable_cache = false
        volumes = ["/cache"]
        shm_size = 0
      [runners.cache]
        [runners.cache.s3]
        [runners.cache.gcs]
```
5. Verify the Runner

    Go to your GitLab project:
        Navigate to Settings > CI/CD > Runners.
        Check if your new runner appears under "Available specific runners."

    Run a pipeline:
        Commit a .gitlab-ci.yml file to your project to start a pipeline and see if the runner picks up the job.

Example .gitlab-ci.yml

Here’s a simple example of a .gitlab-ci.yml file that uses the Docker executor:

```

image: maven:3.8.4-openjdk-11

stages:
  - build

build-job:
  stage: build
  script:
    - mvn --version
    - mvn clean install

```
By following these steps, you should have a GitLab Runner set up on an EC2 instance using the Docker executor. If you need any more help, feel free to ask!




