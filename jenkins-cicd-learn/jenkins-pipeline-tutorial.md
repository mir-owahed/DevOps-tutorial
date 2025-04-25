# 🚀 Jenkins Setup for Docker-Based CI/CD Pipeline

This guide helps you set up a Jenkins environment to:

- Build Docker images
- Push to Docker Hub
- Scan Docker images using Trivy
- Publish HTML security reports

---

## ✅ Prerequisites

- 🐧 Linux host (Ubuntu 22.04 recommended)
- 🐳 Docker installed
- Jenkins installed with Docker socket access

---

## 1️⃣ Install Jenkins on Your Host

### Step 1.1: Update the system

```bash
sudo apt update && sudo apt upgrade -y
```

### Step 1.2: Install Java (Required for Jenkins)

```bash
sudo apt install openjdk-11-jdk -y
```

### Step 1.3: Add Jenkins repo and install Jenkins

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
```

### Step 1.4: Start and enable Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

---

## 2️⃣ Install Docker

### Step 2.1: Install Docker

```bash
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

### Step 2.2: Add Jenkins user to the Docker group

```bash
sudo usermod -aG docker jenkins
```

🔄 Restart Jenkins or reboot the system:

```bash
sudo systemctl restart jenkins
```

---

## 3️⃣ Docker Socket Access for Jenkins

Ensure Jenkins has access to the Docker daemon:

```bash
ls -l /var/run/docker.sock
```

Jenkins should be in the same group (usually `docker`).

---

## 4️⃣ Install Required Jenkins Plugins

Go to: **Manage Jenkins → Plugin Manager → Available**  
Install the following:

| Plugin Name           | Use                                  |
|-----------------------|---------------------------------------|
| Docker Pipeline       | Run Docker containers inside pipeline |
| Pipeline              | Create Jenkins pipelines              |
| HTML Publisher        | Publish Trivy HTML scan report        |
| Credentials Binding   | Bind Docker credentials in pipelines  |

---

## 5️⃣ Add Docker Hub Credentials in Jenkins

Go to: **Manage Jenkins → Credentials → (Global)** → **Add Credentials**

- **Kind**: Username and password
- **ID**: `docker-hub-creds`
- **Username**: Your Docker Hub username
- **Password**: Your Docker Hub password or token

Click **Save** ✅

---

## 🧪 Test Pipeline

Create a simple test pipeline to validate Docker access:

```groovy
pipeline {
    agent {
        docker {
            image 'docker:20.10.7'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Check Docker Version') {
            steps {
                sh 'docker --version'
            }
        }
    }
}
```

✅ If this succeeds, Jenkins has Docker access.

---

## 📋 Summary

| ✅ Setup Task                            | Status |
|------------------------------------------|--------|
| Jenkins installed and running            | ✅     |
| Docker installed and started             | ✅     |
| Jenkins has access to Docker socket      | ✅     |
| Required plugins installed               | ✅     |
| Docker Hub credentials configured        | ✅     |

---

# Jenkins Pipeline Tutorial: Build, Dockerize, Scan & Publish a Java App

This tutorial demonstrates how to set up a Jenkins pipeline using Docker to build a Java application with Maven, Dockerize it, push it to Docker Hub, and scan the Docker image using Trivy.

## 🛠️ Prerequisites

- A running **Jenkins** instance with Docker socket access
- Docker installed on the Jenkins host machine
- Jenkins Plugins installed:
  - Docker Pipeline
  - Pipeline
  - HTML Publisher
  - Credentials Binding
- Docker Hub credentials stored in Jenkins (ID: `docker-hub-creds`)

## 🧪 Jenkinsfile

Below is a complete `Jenkinsfile` for the pipeline:

```groovy
pipeline {
    agent {
        docker {
            image 'abhishekf5/maven-abhishek-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        IMAGE_NAME = 'owahed1/boardgame-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('Get Commit Hash') {
            steps {
                script {
                    env.GIT_TAG = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
                }
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Dockerize') {
            steps {
                sh '''
                    docker --version
                    docker build -t $IMAGE_NAME:$GIT_TAG .
                    docker tag $IMAGE_NAME:$GIT_TAG $IMAGE_NAME:latest
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $IMAGE_NAME:$GIT_TAG
                        docker push $IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Scan Docker Image') {
            steps {
                sh '''
                    mkdir -p trivy-report
                    docker run --rm \
                        -v /var/run/docker.sock:/var/run/docker.sock \
                        -v $PWD/trivy-report:/report \
                        aquasec/trivy:latest image \
                        --format html \
                        --output /report/report.html \
                        --severity CRITICAL,HIGH \
                        $IMAGE_NAME:$GIT_TAG || echo "Scan completed with vulnerabilities."
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'trivy-report/report.html', fingerprint: true

            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'trivy-report',
                reportFiles: 'report.html',
                reportName: 'Trivy Security Report'
            ])
        }

        success {
            echo "✅ Image $IMAGE_NAME:$GIT_TAG pushed and scanned successfully."
        }

        failure {
            echo "❌ Pipeline failed during one or more stages."
        }
    }
}
```

## 📈 Output

- Jenkins builds the Java app
- Docker image is created and pushed to Docker Hub
- Trivy generates an HTML security report
- Report is archived and viewable in Jenkins UI

## 🔐 Security

- Trivy ensures your image is scanned for critical and high vulnerabilities
- Docker Hub credentials are securely managed via Jenkins Credentials Binding

---
# Jenkins Pipeline Tutorial: Build, Dockerize, Scan & Analyze Java App

This tutorial demonstrates how to set up a **Jenkins Pipeline** to:

✅ Clone a Java project from GitHub  
✅ Build the project using Maven  
✅ Dockerize the Java application  
✅ Push the Docker image to Docker Hub  
✅ Scan the image for vulnerabilities using **Trivy**  
✅ Perform static code analysis using **SonarQube**

---

## 🛠 Prerequisites

- ✅ A running Jenkins instance with Docker socket access (`/var/run/docker.sock`)
- ✅ Docker installed on the Jenkins host
- ✅ Jenkins Plugins:
  - Docker Pipeline
  - Pipeline
  - HTML Publisher
  - Credentials Binding
- ✅ Jenkins credentials:
  - `docker-hub-creds` → Docker Hub username and password
  - `sonarqube-token` → SonarQube token
- ✅ A running SonarQube server (e.g., `http://<public-ip>:9000`)
- ✅ The SonarQube project must exist with a generated token

---

## 🔐 Jenkins Credentials Setup

1. Go to **Jenkins → Manage Jenkins → Credentials → Global → Add Credentials**.
2. Create:
   - **Username/Password** type:
     - ID: `docker-hub-creds`
     - Username: your Docker Hub username
     - Password: your Docker Hub password
   - **Secret Text** type:
     - ID: `sonarqube-token`
     - Secret: your SonarQube user token

---

## 🧪 Jenkins Pipeline (`Jenkinsfile`)

```groovy
pipeline {
    agent {
        docker {
            image 'abhishekf5/maven-abhishek-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        IMAGE_NAME = 'owahed1/boardgame-app'
        SONAR_URL = "http://34.201.116.83:9000"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('Get Commit Hash') {
            steps {
                script {
                    env.GIT_TAG = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
                }
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Code Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonarqube-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        mvn sonar:sonar \
                          -Dsonar.projectKey=boardgame-app \
                          -Dsonar.host.url=$SONAR_URL \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }

        stage('Dockerize') {
            steps {
                sh '''
                    docker build -t $IMAGE_NAME:$GIT_TAG .
                    docker tag $IMAGE_NAME:$GIT_TAG $IMAGE_NAME:latest
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $IMAGE_NAME:$GIT_TAG
                        docker push $IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Scan Docker Image') {
            steps {
                sh '''
                    mkdir -p trivy-report
                    docker run --rm \
                        -v /var/run/docker.sock:/var/run/docker.sock \
                        -v $PWD/trivy-report:/report \
                        aquasec/trivy:latest image \
                        --format html \
                        --output /report/report.html \
                        --severity CRITICAL,HIGH \
                        $IMAGE_NAME:$GIT_TAG || echo "Scan completed with vulnerabilities."
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'trivy-report/report.html', fingerprint: true

            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'trivy-report',
                reportFiles: 'report.html',
                reportName: 'Trivy Security Report'
            ])
        }

        success {
            echo "✅ Pipeline completed successfully. Docker image is built, scanned, and pushed."
        }

        failure {
            echo "❌ Pipeline failed."
        }
    }
}


