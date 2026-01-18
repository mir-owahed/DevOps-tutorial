deploy with [Docker](https://github.com/mir-owahed/DevOps-tutorials/blob/Main/docker-learn/docker-installation.md):

```
docker volume create n8n_data
docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```
