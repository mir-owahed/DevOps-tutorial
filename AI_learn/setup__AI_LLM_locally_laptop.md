
# 🧠 Host ALL Your AI Locally — Full Setup Guide

This guide walks you through how to run your own AI stack *completely locally*:
- ✅ No internet required
- 🔐 Fully private and secure
- 🖥️ Works on Linux, macOS, or Windows (via WSL)
- 🧩 Includes chat interface, image generation, and document/chat integrations

---

## 🛠️ Requirements
- Any decent computer (GPU recommended)
- OS: Linux, macOS, or Windows with WSL
- Tools: `ollama`, `docker`, `automatic1111`, `pyenv`

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
sudo docker run -d --name open-webui --network host -e OLLAMA_BASE_URL=http://localhost:11434 ghcr.io/open-webui/open-webui:main
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

## 🔄 Monitor GPU Usage (Optional)
```bash
watch -n 0.5 nvidia-smi
```

---

## 4️⃣ Install Stable Diffusion (Automatic1111)

### ➤ Install `pyenv` and Python 3.10
```bash
sudo apt install make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev curl libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

curl https://pyenv.run | bash

# Add to .bashrc
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"
source ~/.bashrc

pyenv install 3.10
pyenv global 3.10
```

### ➤ Install Stable Diffusion UI
```bash
mkdir stable-diff
cd stable-diff
wget https://raw.githubusercontent.com/AUTOMATIC1111/stable-diffusion-webui/master/webui.sh
chmod +x webui.sh
./webui.sh
```

Visit in browser:
```
http://localhost:7860
```

---

## 🔗 Integrate Stable Diffusion into Open WebUI
- Settings → Image → Add base URL:
```
http://127.0.0.1:7860
```
- Enable “Image Generation”

---

## 5️⃣ Obsidian Notes Integration (Bonus)
- Install **BMO Chatbot** plugin
- Configure:
  - Model: `llama2`
  - Base URL: `http://localhost:11434`

Chat inside your notes with context-awareness and AI-enhanced features.

---

## ✅ Final Thoughts
- Fully **private AI** stack
- Works **offline**
- Ideal for home labs, education, enterprise
- Customize models, run image generation, and reference documents with ease

---

Created based on NetworkChuck's “Host ALL Your AI Locally” tutorial.
