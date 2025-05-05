# How to install jenkins on Linux (Ubuntu)

```bash
sudo apt update
sudo apt install fontconfig openjdk-21-jre
java -version
```
```bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
..........................
Start Jenkins

You can enable the Jenkins service to start at boot with the command:
```sh
sudo systemctl enable jenkins
```
You can start the Jenkins service with the command:
```sh
sudo systemctl start jenkins
```
You can check the status of the Jenkins service using the command:
```sh
sudo systemctl status jenkins
```
You can check the status of the Jenkins service using the command:
```sh
ps -ef | grep jenkins
```
print the password at console
```sh
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Reference:
https://www.jenkins.io/doc/book/installing/linux/

## Install Docker Pipeline plugin in Jenkins:
## Setup Docker Containers As Build Agents:
*  Go to Manage Jenkins > Manage Plugins.
* In the Available tab, search for "Docker Pipeline".
*  Select the plugin and click the Install button.
*  Restart Jenkins after the plugin is installed.

## Docker Slave Configuration:
```sh
sudo apt update
sudo apt install docker.io
```
## Grant Jenkins user and Ubuntu user permission to docker:
```sh
sudo groupadd docker
sudo usermod -aG docker $USER
sudo usermod -aG docker ubuntu [ubuntu is name of the user of vps server]
sudo usermod -aG docker jenkins
newgrp docker
sudo systemctl restart docker

ps -ef | grep jenkins
```
## Restart Jenkins:
```sh
http://<ec2-instance-public-ip>:8080/restart
```
### Jenkins pipeline 
pipeline script from SCM
Use docker as agent
```
### Plugin
```
Manage jenkins > available plugin > sonar scanner
```
### Install sonar server on ec2


