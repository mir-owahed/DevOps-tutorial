```
mir@ubuntu-vbox:~$ history

    1  sudo su

    2  sudo visudo

    3  visudo

    4  su -

    5  su - root

    6  sudo apt install nano

    7  java --version

    8  sudo apt install maven

    9  maven --version

   10  java --version

   11  mvn --version

   12  lsb_release -a

   13  sudo wget -O /usr/share/keyrings/jenkins-keyring.asc   https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

   14  echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]"   https://pkg.jenkins.io/debian-stable binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null

   15  sudo apt-get update

   16  sudo apt-get install jenkins

   17  sudo systemctl enable jenkins

   18  sudo systemctl start jenkins

   19  sudo systemctl status jenkins

   20  sudo cat /var/lib/jenkins/secrets/initialAdminPassword

   21  ls

   22  git -version

   23  sudo apt install git

   24  git clone https://github.com/mir-owahed/SRE101.git

   25  ls

   26  cd SRE101/

   27  ls

   28  cd

   29  sudo rm -rf /usr/local/go && tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz

   30  sudo rm -rf /usr/local/go && tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz

   31  sudo rm -rf /usr/local/go

   32  sudo tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz

   33  export PATH=$PATH:/usr/local/go/bin

   34  go version

   35  cd

   36  go version

   37  sudo apt-get install wget gpg

   38  wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg

   39  sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg

   40  echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null

   41  rm -f packages.microsoft.gpg

   42  sudo apt install apt-transport-https

   43  sudo apt update

   44  sudo apt install code

   45  code .

   46  go run hello.go 

   47  go version

   48  vim install-docker.sh

   49  sudo apt install vim

   50  sudo vim install-docker.sh

   51  ls

   52  sudo su

   53  chmod +x install_docker.sh

   54  chmod +x install-docker.sh

   55  sudo chmod +x install-docker.sh

   56  ./install-docker.sh 

   57  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

   58  sudo groupadd docker

   59  sudo usermod -aG docker $USER

   60  newgrp docker

   61  docker version

   62  docker --version

   63  docker help

   64  docker ps help

   65  docker ps --help 

   66  docker ps -a

   67  docker ps

   68  history

mir@ubuntu-vbox:~$ 




```
