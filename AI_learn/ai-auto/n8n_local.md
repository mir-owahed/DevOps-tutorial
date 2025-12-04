```
sudo docker volume create n8n_data

```

```
sudo docker run -d  \
 --name n8n \
 -p 5678:5678 \
 -e GENERIC_TIMEZONE="Asia/Kolkata" \
 -e TZ="Asia/Kolkata" \
 -e N8N_SECURE_COOKIE=false
 -v n8n_data:/home/mir/.n8n \
 docker.n8n.io/n8nio/n8n
```
