## 🔄 Jenkins Pipeline Stage: Update `deployment-service.yaml` with Docker Image Tag

This stage updates the Kubernetes deployment manifest `deployment-service.yaml` with the latest Docker image tag and pushes the change to the GitHub repository [`mir-owahed/Boardgame`](https://github.com/mir-owahed/Boardgame.git).

### ✅ Pipeline Stage Code

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
        SONAR_URL = "http://localhost:9000"
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

        stage('Update Deployment File & Push to GitHub') {
    environment {
        GIT_REPO_NAME = "Boardgame"
        GIT_USER_NAME = "mir-owahed"
    }
    steps {
        withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
            sh '''
                git config user.email "bachchu333@gmail.com"
                git config user.name "Mir Owahed Ali"

                # Update image tag in deployment-service.yaml
                sed -i "s|image: owahed1/boardgame-app:.*|image: owahed1/boardgame-app:${GIT_TAG}|" deployment-service.yaml

                git add deployment-service.yaml
                git commit -m "🔄 Update image tag in deployment-service.yaml to ${GIT_TAG}"
                
                git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME}.git HEAD:main
            '''
        }
    }
}

   
    }
}
```
## 🔐 Required Jenkins Credential

To allow Jenkins to push changes to your GitHub repository, add the following credential:

1. Navigate to: **Jenkins → Manage Jenkins → Credentials → Global → Add Credentials**
2. Fill in the details as follows:

| Field        | Value                                               |
|--------------|-----------------------------------------------------|
| **Kind**     | Secret Text                                         |
| **ID**       | `github-token`                                      |
| **Secret**   | _Your GitHub Personal Access Token (with `repo` scope)_ |
| **Description** | GitHub token for push access                    |

📌 **Note:** Make sure the GitHub token has the `repo` scope enabled to allow pushing commits to your repositories.
