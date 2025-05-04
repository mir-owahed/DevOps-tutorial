# Jenkins pipeline for java based app and use docker container as build agent
```
pipeline {
    agent {
        docker {
        image 'maven:3.8.7-openjdk-18-slim'
  }
}
    stages {
        stage('checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }
        
        stage('check version') {
            steps {
                sh '''
                mvn --version
                java --version
                '''
            }
        }
        
        stage('compile') {
            steps {
                sh 'mvn validate'
            }
        }
        
        stage('package') {
            steps {
                sh 'mvn clean package'
            }
        }
        
    }
}
```
```
pipeline {
     agent {
    docker {
      image 'abhishekf5/maven-abhishek-docker-agent:v1'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }

    environment {
        DOCKER_IMAGE = 'boardgame-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mir-owahed/Boardgame.git'
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
                    docker build -t $DOCKER_IMAGE .
                '''
            }
        }
    }
}

```
Jenkins pipeline, uses docker container as agent, image scan with trivy
```
pipeline {
     agent {
    docker {
      image 'abhishekf5/maven-abhishek-docker-agent:v1'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }

    environment {
        DOCKER_IMAGE = 'boardgame-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mir-owahed/Boardgame.git'
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
                    docker build -t $DOCKER_IMAGE .
                '''
            }
        }
        
        stage('Scan Docker Image') {
    steps {
        sh '''
            docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy:latest image --exit-code 1 --severity CRITICAL,HIGH $DOCKER_IMAGE || echo "Scan completed with vulnerabilities."
        '''
    }
}

        
    }
}

```
trivy scan with report
```
pipeline {
    agent {
        docker {
            image 'abhishekf5/maven-abhishek-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        DOCKER_IMAGE = 'boardgame-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mir-owahed/Boardgame.git'
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
                    docker build -t $DOCKER_IMAGE .
                '''
            }
        }

        stage('Scan Docker Image') {
            steps {
                sh '''
                    mkdir -p trivy-report
                    docker run --rm \
                      -v /var/run/docker.sock:/var/run/docker.sock \
                      -v $(pwd)/trivy-report:/root/reports \
                      aquasec/trivy:latest \
                      image --format template \
                      --template "@contrib/html.tpl" \
                      -o /root/reports/report.html \
                      $DOCKER_IMAGE || echo "Scan completed with findings."
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'trivy-report/report.html', fingerprint: true
        }
    }
}

```
push the image with docker hub
```
pipeline {
    agent {
        docker {
            image 'abhishekf5/maven-abhishek-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        DOCKER_IMAGE = 'boardgame-app:jenkins'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mir-owahed/Boardgame.git'
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
                    docker build -t $DOCKER_IMAGE .
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker tag $DOCKER_IMAGE $DOCKER_USER/boardgame-app:jenkins
                        docker push $DOCKER_USER/boardgame-app:jenkins
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
                        $DOCKER_IMAGE || echo "Scan completed with vulnerabilities."
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
    }
}

```
generate a unique tag per build
```
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
        stage('checkout') {
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
```
pipeline {
    agent {
        docker {
            image 'docker:20.10.7'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        IMAGE_NAME = 'owahed1/boardgame-app'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('Check Docker Version') {
            steps {
                sh 'docker --version'
            }
        }

        stage('Build Docker Image with Build Number Tag') {
            steps {
                sh '''
                    echo "Building Docker image with tag: $BUILD_NUMBER"
                    docker build -t $IMAGE_NAME:$BUILD_NUMBER .
                    docker tag $IMAGE_NAME:$BUILD_NUMBER $IMAGE_NAME:latest
                '''
            }
        }

        stage('List Docker Images') {
            steps {
                sh 'docker images'
            }
        }
    }
}

```
```
pipeline {
    agent {
        docker {
            image 'owahed1/maven-mir-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('check version') {
            steps {
                sh '''
                mvn --version
                java --version
                '''
            }
        }
        
        
        stage('Check Docker Version') {
            steps {
                sh 'docker --version'
            }
        }

        
    }
}

```
```
pipeline {
    agent {
        docker {
            image 'owahed1/maven-mir-docker-agent:v1'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('check version') {
            steps {
                sh '''
                mvn --version
                java --version
                '''
            }
        }
        
        
        stage('Check Docker Version') {
            steps {
                sh 'docker --version'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        
    }
}

```
```
pipeline {
    agent {
        docker {
            image 'owahed1/maven-mir-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        IMAGE_NAME = 'owahed1/boardgame-app'
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
    }

    post {
        success {
            echo "✅ Docker image $IMAGE_NAME:$BUILD_NUMBER built and tagged as latest."
        }
        failure {
            echo "❌ Pipeline failed."
        }
    }
}

```
## 🚀 Jenkins Pipeline to Build and Push Docker Image Using DinD
```
pipeline {
    agent {
        docker {
            image 'owahed1/maven-mir-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        IMAGE_NAME = 'owahed1/boardgame-app'
        DOCKER_HUB_CREDENTIALS_ID = 'docker-hub-credentials'  // Jenkins Credentials ID for Docker Hub
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
            echo "✅ Docker image $IMAGE_NAME:$BUILD_NUMBER pushed to Docker Hub."
        }
        failure {
            echo "❌ Pipeline failed."
        }
    }
}
```
📋 Jenkins Credential Setup

    Go to: Jenkins → Manage Jenkins → Credentials → Global → Add Credentials

    Kind: Username and Password

    ID: docker-hub-credentials

    Username: Your Docker Hub username

    Password: Your Docker Hub password or access token

    Description: Docker Hub credentials for pushing images

```
pipeline {
    agent {
        docker {
            image 'owahed1/maven-mir-docker-agent:v1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        IMAGE_NAME = 'owahed1/boardgame-app'
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

        stage('Dockerize') {
            steps {
                sh """
                    echo "Building Docker image: $IMAGE_NAME:$BUILD_NUMBER"
                    docker build -t $IMAGE_NAME:$BUILD_NUMBER .
                    docker tag $IMAGE_NAME:$BUILD_NUMBER $IMAGE_NAME:latest
                """
            }
        }

        stage('Push to Docker Hub') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'docker-hub-creds',
                                     usernameVariable: 'DOCKER_USER',
                                     passwordVariable: 'DOCKER_PASS')]) {
      sh '''
        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
        docker push $IMAGE_NAME:$BUILD_NUMBER
      '''
    }
  }
}


    }

    post {
        success {
            echo "✅ Docker image $IMAGE_NAME:$BUILD_NUMBER built and tagged as latest."
        }
        failure {
            echo "❌ Pipeline failed."
        }
    }
}


```
```
pipeline {
    agent {
        docker {
            image 'docker:20.10.7-dind'
            args '--privileged -v /var/run/docker.sock:/var/run/docker.sock --user root'
        }
    }

    environment {
        IMAGE_NAME = 'owahed1/boardgame-app'
    }

    stages {
        stage('Start Docker Daemon') {
            steps {
                sh '''
                    dockerd-entrypoint.sh > /tmp/docker.log 2>&1 &
                    sleep 10
                    docker version
                '''
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    changelog: false,
                    poll: false,
                    url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('Install Maven') {
            steps {
                sh '''
                    apk add --no-cache maven openjdk11
                    mvn --version
                    java --version
                '''
            }
        }

        

        stage('Dockerize') {
            steps {
                sh '''
                    echo "Building Docker image: $IMAGE_NAME:$BUILD_NUMBER"
                    docker build -t $IMAGE_NAME:$BUILD_NUMBER .
                    docker tag $IMAGE_NAME:$BUILD_NUMBER $IMAGE_NAME:latest
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Docker image $IMAGE_NAME:$BUILD_NUMBER built and tagged as latest."
        }
        failure {
            echo "❌ Pipeline failed."
        }
    }
}

```
Multi-stage Multi-agent pipeline

```
pipeline {
    agent none

    stages {
        stage('Checkout') {
            agent {
                docker {
                    image 'maven:3.8.7-openjdk-18-slim'
                }
            }
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('Check Versions') {
            agent {
                docker {
                    image 'maven:3.8.7-openjdk-18-slim'
                }
            }
            steps {
                sh '''
                    mvn --version
                    java --version
                '''
            }
        }

        stage('Compile') {
            agent {
                docker {
                    image 'owahed1/maven-mir-docker-agent:v1'
                    args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh 'mvn validate'
            }
        }

        stage('Package') {
            agent {
                docker {
                    image 'owahed1/maven-mir-docker-agent:v1'
                    args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh 'mvn clean package'
            }
        }
    }
}

```
