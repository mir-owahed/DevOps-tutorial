
# 🧠 Run AI LLM on locally on laptop.

This guide walks you through how to run your own AI stack *completely locally*:
- ✅ No internet required
- 🔐 Fully private and secure
- 🖥️ Works on Linux, macOS, or Windows (via WSL)


---

## 🛠️ Requirements
- Any decent computer (GPU recommended)
- OS: Linux, macOS, or Windows with WSL
- Tools: `ollama`, `docker`
---

## 1️⃣ Install Ollama (AI Model Backend)

### ➤ On Windows:
```bash
wsl --install
```

### ➤ On Ubuntu (in WSL or native):
```bash
sudo apt update
sudo apt upgrade -y
curl -fsSL https://ollama.com/install.sh | sh
```

### ➤ Test Ollama API
Visit in browser:
```
http://localhost:11434
```

### ➤ Pull and Run a Model
```bash
ollama pull llama2
ollama run llama2
```

---

## 2️⃣ Set Up Open WebUI (Chat Interface for Ollama)

### ➤ Install Docker on Ubuntu
```bash
sudo apt update
sudo apt install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### ➤ Run Open WebUI Container
```bash
sudo docker run -d --name open-webui --network=host -e OLLAMA_BASE_URL=http://127.0.0.1:11434 ghcr.io/open-webui/open-webui:main
sudo docker run -d -p 3000:8080 --network=host -e OLLAMA_BASE_URL=http://localhost.1:11434 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
sudo docker run -d --network=host -e OLLAMA_BASE_URL=http://127.0.0.1:11434 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

```

Visit in browser:
```
http://localhost:8080
```

---

## 3️⃣ Download & Switch AI Models
```bash
ollama pull codellama
```
Switch models via dropdown or `@modelname` in chat.

---

## 🔒 Customize Prompts / Add Guardrails
- Create custom model files in Open WebUI
- Example system prompt:
```
You are an educational assistant. Do not help with cheating or writing essays.
```

---

## 📄 Use Documents in Chat
- Upload documents in Open WebUI → Documents
- Use `#filename` in your prompts:
```markdown
#example_doc
Summarize this document.
```

---


---

## ✅ Final Thoughts
- Fully **private AI** stack
- Works **offline**
- Ideal for home labs, education, enterprise
- Customize models, run image generation, and reference documents with ease

---

