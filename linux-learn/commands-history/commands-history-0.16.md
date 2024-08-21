History of commands used in ubuntu
```
mir@ubuntu22-vbox:~/Downloads/helloApp$ history
sudo su
su -
su - root
cd
history
su root
su -
sudo su
sudo visudo
su -
sudo apt update
sudo apt-get install wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg
sudo apt install apt-transport-https
sudo apt update
sudo apt install code
ls
cd Documents/
ls
mkdir python-app
cd python-app/
code .
curl http://localhost:81
sudo apt install curl
curl http://localhost:81
curl http://localhost:81/ping
curl http://localhost:81/hello
curl http://localhost:81/ping
curl http://localhost:81/hello
curl http://localhost:81/ping
curl http://localhost:81/
history
cd Documents/python-app/
history
history >> commands.txt 
python3 -V
pip3 -V
sudo apt install python3 python3-pip build-essential python3-dev
python3 -V
pip3 -V
sudo pip3 install -r requirements.txt
python3 app.py 
sudo pip3 install -r requirements.txt
python3 app.py 
sudo pip3 install flask
python3 app.py 
sudo python3 app.py 
history > commands.txt
ls
history
git -V
git --version
git remote -V
git init
git status
git add .
git status
git commit -m "python flask app"
git log
git remote -V
git remote -v
git log
git branch -M main
git log
git remote add origin https://github.com/mir-owahed/python-flask-app.git
git remote -v
git push -u origin main
history
git status
git commit -am "commands updated"
git status
git push -u origin main
node -v
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
nvm install node
command -v nvm
nvm install node
npm -v
node app.js 
history
node app.js 
code .
history
ls
history
exit
curl http://localhost:8080
java --version
sudo apt install openjdk-11-jdk-headless
java --version
mvn --version
sudo apt install maven
mvn --version
mvn compile
javac --version
java 17
sudo apt install openjdk-17-jdk
mvn compile
ls
mvn package
ls
cd target/
ls
java -jar javaSpringProj-0.0.1-SNAPSHOT.jar 
curl http://localhost:8080/
curl http://localhost:8080
java -jar javaSpringProj-0.0.1-SNAPSHOT.jar 
mvn test
mvn clean package
cd ..
mvn test
cd target/
ls
java -jar javaSpringProj-0.0.1-SNAPSHOT.jar 
cd ..
mvn clean package
ls
mvn test
mvn clean package
java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 
history
ls
mv javaSpringProj.zip  ~/Documents/
ls
cd 
cd Documents/
ls
unzip javaSpringProj.zip 
ls
cd javaSpringProj/
ls
code .
history
curl 127.0.0.1:9000
ls
cd target/
ll
ls
mvn test
cd ..
mvn compile
mvn test
mvn clean package
java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 
mvn clean package
java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 
ls
cd target/
ls
cd ..
mvn clean package
java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 
mvn test
mvn clean
mvn test
mvn clean
mvn clean package
java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 
history
code .
npm run dev
npm run build
npm run dev
npm run build
npm run dev
npm run build
npm run dev
npm run build
git init
git status
git add .
git commit "react frontend hello world app"
git commit -m "react frontend hello world app"
git status
git remote -v
git remote -V
git remote -v
git remote add origin https://github.com/mir-owahed/react-app.git
git remote -v
git npx create-next-app@latest
cd react-app/
code .
npm run dev
npm run build
npm start
code .
docker ps
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
# Add the repository to Apt sources:
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo groupadd docker
sudo usermod -aG $USER
sudo usermod -aG docker $USER
docker help
clear
docker --version
docker ps 
sudo usermod -aG docker $USER
docker ps -a
minikube start --nodes 2
kubectl --help
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
kubectl --help
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
ls
kubectl --help
ls -la
clear
ls -la
vim .config/
sudo apt install vim
vim .config/
ls -a
vim .bashrc 
k get nodes
docker ps
sudo groupadd docker
newgrp docker
kubectl get nodes
k get nodes
vim .bashrc 
k get nodes
k config get-clusters
k get namespaces
ls
cd Documents/
ls
mkdir k8s
cd k8s/
docker ps
cd Documents/
ls
cd k8s/
ls
kubectl get nodes
docker ps
docker ps -a
docker ps
minikube start
helm repo add bitnami https://charts.bitnami.com/bitnami
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
minikube status
ls
go version
cd Downloads/
ls
tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz 
sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz 
clear
export PATH=$PATH:/usr/local/go/bin
go version
cd /usr/local/go/bin
ls
export PATH=$PATH:/usr/local/go/bin
exit
go mod init hello.go 
cat go.mod 
go build hello.go 
ls
./hello 
go version
sudo export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:/usr/local/go/bin
ls
go version
cd Downloads/
ls
cd
cd Documents/
ls
mkdir go-app
cd go-app/
code .
ls
Cd Documents/
cd Documents/
ls
cd DevOps-tutorial/
ls
cd ..
https://github.com/spring-projects/spring-petclinic.git
git clone https://github.com/spring-projects/spring-petclinic.git
ls
cd spring-petclinic/
ls
java --version
mvn --version
javac --version
mvn compile
mvn package
java -jar target/spring-petclinic-3.3.0-SNAPSHOT.jar 
mvn test
code .
java -jar target/spring-petclinic-3.3.0-SNAPSHOT.jar 
java -jar target/spring-petclinic-3.3.0-SNAPSHOT.jar --httpPort=9001
ls
cd Documents/
ls
git clone https://github.com/mir-owahed/Task-Master-Pro.git
ls
cd Task-Master-Pro/
ls
mvn compile
mvn test
mvn package
ls
cd target/
ls
java -jar todo-app-1.0-SNAPSHOT.jar 
ls
cd Documents/
git clone https://github.com/iam-veeramalla/go-web-app.git
ls
cd go-web-app/
ls
go run main.go 
go version
curl https://go.dev/dl/go1.22.5.linux-amd64.tar.gz
wget https://go.dev/dl/go1.22.5.linux-amd64.tar.gz
ls
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version
exit
go version
export PATH=$PATH:/usr/local/go/bin
go version
sudo export PATH=$PATH:/usr/local/go/bin
go version
sudo nano .bashrc
go version
```
