setup n8n at DO
```
1  uname -a
    2  sudo apt update
    3  sudo apt upgrade
    4  # Add Docker's official GPG key:
    5  sudo apt-get update
    6  sudo apt-get install ca-certificates curl
    7  sudo install -m 0755 -d /etc/apt/keyrings
    8  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    9  sudo chmod a+r /etc/apt/keyrings/docker.asc
   10  # Add the repository to Apt sources:
   11  echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   12  sudo apt-get update
   13  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   14  docker version
   15  docker compose version
   16  git version
   17  git clone https://github.com/n8n-io/n8n-docker-caddy.git
   18  ls
   19  cd n8n-docker-caddy/
   20  sudo docker volume create caddy_data
   21  sudo docker volume create n8n_data
   22  sudo ufw allow 80
   23  sudo ufw allow 443
   24  nano .env
   25  ls
   26  sudo docker volume create caddy_data
   27  sudo docker volume create n8n_data
   28  ls
   29  nano .env
   30  ls
   31  nano docker-compose.yml 
   32  nano caddy_config/Caddyfile
   33  sudo docker compose up -d
   34  pwd
   35  nano .env
   36  sudo docker compose stop
   37  sudo docker compose up -
```
