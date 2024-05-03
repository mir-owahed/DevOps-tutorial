vim install_docker.sh
```
#!/bin/bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
make executable
```
chmod +x install_docker.sh
```
Run the script
```
./ install_docker.sh
```
Install the Docker packages:
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Verify that the Docker Engine installation is successful by running the hello-world image:
```
sudo docker run hello-world
```
Post-installation
```
sudo groupadd docker
sudo usermod -aG docker $USER
sudo usermod -aG docker ubuntu [ubuntu is name of the user of vps server]
```
Let's play
```
docker --version
docker help
docker ps -a
```
