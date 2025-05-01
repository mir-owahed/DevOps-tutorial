# 🚀 Jenkins Master-Slave (Controller-Agent) Setup on AWS EC2

Setting up a Jenkins Master-Slave (Controller-Agent) architecture on AWS EC2 allows you to distribute build tasks efficiently. Below is a step-by-step guide to help you set up Jenkins Master-Slave on EC2 instances:

---

## ✅ Prerequisites

- 2 EC2 instances:
  - **Master** (Jenkins Controller)
  - **Slave** (Jenkins Agent)

- OS: Ubuntu 20.04/22.04 (recommended)

- Security group allowing:
  - Port **8080** (for Jenkins UI)
  - Port **22** (for SSH)
 
 - EC2 Key Pairs:

    - controller-key.pem: For SSH access to Jenkins Controller

    - agent-key.pem: For SSH access to Jenkins Agent

- Java installed on both EC2s (OpenJDK 11 or higher)

---

## 🔧 Step 1: Install Jenkins on the Master EC2

SSH into your **Master EC2** and run:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

Access Jenkins at: `http://<Master_Public_IP>:8080`

---

## 🔐 Step 2: Unlock Jenkins and Install Plugins

- Run the following to get the initial admin password:

  ```bash
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  ```

- Complete the setup wizard.

- Install **suggested plugins**.

- Create an **admin user**.

---

## 💻 Step 3: Prepare the Slave EC2 (Agent)

SSH into the **Slave EC2** and run:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```

(Optional) Create a `jenkins` user on the agent:

```bash
sudo adduser jenkins
```
## 🔐 Step 4: Setup SSH from Jenkins Master to Agent

Copy the agent-key.pem
chmod 400 agent-key.pem
ssh -i agent-key.pem ubuntu@agent-ip

...
# 🚀 Jenkins Master-Slave (Controller-Agent) Setup on AWS EC2

Setting up a Jenkins Master-Slave (Controller-Agent) architecture on AWS EC2 allows you to distribute build tasks efficiently. Below is a step-by-step guide to help you set up Jenkins Master-Slave on EC2 instances:

---

## ✅ Prerequisites

- 2 EC2 instances:
  - **Master** (Jenkins Controller)
  - **Slave** (Jenkins Agent)

- OS: Ubuntu 20.04/22.04 (recommended)

- Security group allowing:
  - Port **8080** (for Jenkins UI)
  - Port **22** (for SSH)

- Java installed on both EC2s (OpenJDK 11 or higher)

---

## 🔧 Step 1: Install Jenkins on the Master EC2

SSH into your **Master EC2** and run:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

Access Jenkins at: `http://<Master_Public_IP>:8080`

---

## 🔐 Step 2: Unlock Jenkins and Install Plugins

- Run the following to get the initial admin password:

  ```bash
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  ```

- Complete the setup wizard.

- Install **suggested plugins**.

- Create an **admin user**.

---

## 💻 Step 3: Prepare the Slave EC2 (Agent)

SSH into the **Slave EC2** and run:

```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```

(Optional) Create a `jenkins` user on the agent:

```bash
sudo adduser jenkins
```

---

## 🔐 Step 4: Setup SSH from Jenkins Master to Agent

### ✅ 1. Ensure You're the Jenkins User on Master

```bash
sudo su - jenkins
```

### ✅ 2. Generate SSH Key (if not already done)

```bash
ssh-keygen -t rsa -b 4096
```

(Press Enter to accept default path and **no passphrase**)

### ✅ 3. Check the Public Key

```bash
cat ~/.ssh/id_rsa.pub
```

You should see something like:

```
ssh-rsa AAAAB3... jenkins@hostname
```

### ✅ 4. Copy Public Key to Slave EC2

SSH into the **slave**:

```bash
ssh -i your-key.pem ubuntu@<slave-public-ip>
```

Then run:

```bash
mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys
```

Paste the **public key** from the master (`id_rsa.pub`) into that file.

Set correct permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

### ✅ 5. Test SSH Access From Jenkins Master

Back on the master (as `jenkins` user):

```bash
ssh ubuntu@<slave-public-ip>
```

If it connects **without asking for a password**, SSH is working.

---

## 🔑 Step 5: Configure Jenkins to Use the SSH Key

### ✅ Get the Private Key

SSH into Jenkins Master:

```bash
ssh -i jenkins-key.pem ubuntu@<master-public-ip>
```

Switch to Jenkins user:

```bash
sudo su - jenkins
```

Check for keys:

```bash
ls -l ~/.ssh/
```

You should see:

- `id_rsa` — private key (keep secure!)
- `id_rsa.pub` — public key

Display private key:

```bash
cat ~/.ssh/id_rsa
```

Copy the **entire content**, including:

```
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

---

### 🔐 Add SSH Credentials in Jenkins

In the **Jenkins Web UI**:

1. Go to: **Manage Jenkins** > **Manage Credentials** > (global) > **Add Credentials**
2. **Kind**: `SSH Username with private key`
3. **Username**: `ubuntu`
4. **Private Key**: `Enter directly` → Paste the private key from above
5. **ID** (optional): `jenkins-slave-key`
6. Click **Save**

---

### ✅ Step 6: Add a New Node (Agent) in Jenkins

1. Go to **Manage Jenkins** > **Nodes** > **New Node**
2. Name: `slave-agent-1`
3. Type: `Permanent Agent`
4. Configure:
   - **# of executors**: 1 or more
   - **Remote root directory**: `/home/ubuntu`
   - **Labels**: `linux` (or any label you want)
   - **Launch method**: `Launch agents via SSH`
   - **Host**: `<slave-public-ip>`
   - **Credentials**: Select the one you just created (e.g., `jenkins-slave-key`)
5. Click **Save** and then **Launch Agent**

---

✅ **Your Jenkins Master-Slave Setup is Complete!** You can now assign jobs to run on the slave using label-based `agent` blocks.

---

