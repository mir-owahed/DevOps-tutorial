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
env file
```
# Replace <directory-path> with the path where you created folders earlier
DATA_FOLDER=/root/n8n-docker-caddy

# The top level domain to serve from, this should be the same as the subdomain you created above
DOMAIN_NAME=learn-with-mir.online
# The subdomain to serve from
SUBDOMAIN=ai

# DOMAIN_NAME and SUBDOMAIN combined decide where n8n will be reachable from
# above example would result in: https://n8n.example.com

# Optional timezone to set which gets used by Cron-Node by default
# If not set New York time will be used
GENERIC_TIMEZONE=Europe/Berlin

# The email address to use for the SSL certificate creation
SSL_EMAIL=bachchu333@gmail.com
```
update
```
40  sudo docker compose stop
   41  docker compose pull
   42  docker compose down
   43  docker compose up -d
```
Caddyfile
```
ai.learn-with-mir.online {
    reverse_proxy n8n:5678 {
      flush_interval -1
    }
}
```
n8n supabase integration
```
select project > Project Setting > Data API > Copy project url > paste it on Supabase Host.
API Keys > Legacy anon, service_role API keys > Copy service_role secret > Paste it on Service Role Secret in n8n.
```
```
copy SQL command > Supabase SQL Editor  and paste it.
Go to Table editor > Click Documents table. > Enable RLS for security reason.
```
Add chat memory at n8n in postgres supabase
```
Click on connect > Transaction pooler > view parameter > Copy host and user and paste it n8n, password will be the password of the project creation.
```
