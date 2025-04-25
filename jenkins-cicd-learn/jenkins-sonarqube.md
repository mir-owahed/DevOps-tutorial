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


```
