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
