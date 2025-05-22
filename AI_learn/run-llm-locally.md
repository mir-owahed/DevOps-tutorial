Run LLMs on local PC
```
mir@DESKTOP-JASRD4A:~$ sudo docker volume create ollama_data
  877  docker run -d -v ollama_data:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
  878  docker ps
  
  883  docker exec -it ollama ollama run llama3.2:1b
  884  docker exec ollama ollama run llama3.2:1b
  885  docker exec ollama ollama ps
  886  docker exec ollama ollama ls
  887  curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "Why is the sky blue?"
}'
  888  curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2:1b",
  "prompt": "Why is the sky blue?"
}'
  mir@DESKTOP-JASRD4A:~$  docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
  mir@DESKTOP-JASRD4A:~$  curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt":"Why is the sky blue?"
}'
  mir@DESKTOP-JASRD4A:~$  curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2:1:1b",
  "prompt":"Why is the sky blue?"
}'
  mir@DESKTOP-JASRD4A:~$  curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2:1b",
  "prompt":"Why is the sky blue?"
}'
  
mir@DESKTOP-JASRD4A:~$

 mir@DESKTOP-JASRD4A:~$ curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2:1b",
  "prompt": "Why is the sky blue?",
  "stream": false
}'
  mir@DESKTOP-JASRD4A:~$  curl -X POST http://localhost:11434/api/generate -H "Content-Type: application/json" -d '{
  "model": "llama3.2:1b",
  "prompt": "Ollama is 22 years old and is busy saving the world. Respond using JSON",
  "stream": false,
  "format": {
    "type": "object",
    "properties": {
      "age": {
        "type": "integer"
      },
      "available": {
        "type": "boolean"
      }
    },
    "required": [
      "age",
      "available"
    ]
  }
}'
```
