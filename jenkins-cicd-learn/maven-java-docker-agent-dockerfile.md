Dockerfile
```
# Use the Eclipse Temurin OpenJDK 17 base image
FROM eclipse-temurin:17-jdk

# Ensure UTF-8 locale
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

# (Optional) switch to a closer Debian mirror:
# RUN sed -i 's|http://deb.debian.org/debian|http://ftp.us.debian.org/debian|g' /etc/apt/sources.list

# Install Maven, Git, and other utilities in one layer
RUN apt-get update && \
    apt-get install -y --no-install-recommends --fix-missing \
      maven \
      git \
      curl \
      ca-certificates \
      gnupg2 \
      lsb-release \
      tar && \
    rm -rf /var/lib/apt/lists/*

# Install Docker CLI only (no daemon) by downloading the static binary
RUN curl -fsSL https://download.docker.com/linux/static/stable/x86_64/docker-25.0.0.tgz \
    | tar -xz --strip-components=1 -C /usr/local/bin docker/docker

# Create a docker group and a non-root 'jenkins' user for safer execution
RUN groupadd -g 1001 docker && \
    useradd -m -u 1001 -g docker jenkins

# Switch to non-root user
USER jenkins

# Set working directory
WORKDIR /workspace

# Default command: display Maven version (override as needed)
CMD ["mvn", "--version"]

```
```
sudo nano Dockerfile
docker build -t owahed1/maven-mir-docker-agent:v1 .
docker login -u owahed1
provide PAT
docker push owahed1/maven-mir-docker-agent:v1
```
# 🚀 Boardgame Java Application CI/CD Pipeline using Jenkins, Docker, and Docker Hub

This project demonstrates a full CI/CD workflow for a **Java Maven** application:  
- Build the project using Maven
- Dockerize it using **Docker-in-Docker (DinD)**
- Push the built Docker image to **Docker Hub**

---

## 📁 Project Repository

[Boardgame Java Application Repository](https://github.com/mir-owahed/Boardgame.git)

---

## 🛠️ Jenkins Pipeline Overview

The Jenkins pipeline consists of the following stages:

1. **Checkout Code**: Clone the GitHub repository.
2. **Check Versions**: Print Maven, Java, and Docker versions.
3. **Build Java Project**: Run `mvn clean package`.
4. **Dockerize (DinD)**: Build and tag the Docker image.
5. **Push to Docker Hub**: Push the image to your Docker Hub repository.

---

## 📜 Jenkins Pipeline Script

```groovy
pipeline {
    agent {
        docker {
            image 'owahed1/maven-mir-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        IMAGE_NAME = 'owahed1/boardgame-app'
        DOCKER_HUB_CREDENTIALS_ID = 'docker-hub-credentials'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    changelog: false,
                    poll: false,
                    url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('Check Versions') {
            steps {
                sh '''
                    mvn --version
                    java --version
                    docker --version
                '''
            }
        }

        stage('Build Java Project') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Dockerize (DinD)') {
            agent {
                docker {
                    image 'docker:20.10.7-dind'
                    args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh """
                    echo "Building Docker image: $IMAGE_NAME:$BUILD_NUMBER"
                    docker build -t $IMAGE_NAME:$BUILD_NUMBER .
                    docker tag $IMAGE_NAME:$BUILD_NUMBER $IMAGE_NAME:latest
                """
            }
        }

        stage('Push to Docker Hub') {
            agent {
                docker {
                    image 'docker:20.10.7-dind'
                    args '--privileged -v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_HUB_CREDENTIALS_ID}", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh '''
                        echo "🔐 Logging into Docker Hub"
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin

                        echo "📦 Pushing Docker image: $IMAGE_NAME:$BUILD_NUMBER"
                        docker push $IMAGE_NAME:$BUILD_NUMBER

                        echo "📦 Pushing Docker image: $IMAGE_NAME:latest"
                        docker push $IMAGE_NAME:latest

                        echo "🚪 Logging out from Docker Hub"
                        docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "✅ Docker image $IMAGE_NAME:$BUILD_NUMBER pushed successfully!"
        }
        failure {
            echo "❌ Pipeline failed."
        }
    }
}

