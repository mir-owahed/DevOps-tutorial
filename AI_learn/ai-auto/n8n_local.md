deploy with [Docker](https://github.com/mir-owahed/DevOps-tutorials/blob/Main/docker-learn/docker-installation.md):

```
docker volume create n8n_data
docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

Self-hosted n8n

```
.................
# Add credentials at n8n
............................
# Add postgres credential in n8n. host: postgres
ports:
      - 5432:5432

# Qdrant URL : http://qdrant:6333/

# Ollama Base URL : http://ollama:11434
```
Commands
```
docker compose --profile cpu up -d
docker compose --profile cpu down
docker ps
docker ps -a

```

<https://gist.github.com/mir-owahed/0e31e8c229fff07ee770e2a7c3da3bb8>
