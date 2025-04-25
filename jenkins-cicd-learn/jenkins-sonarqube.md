Here is your complete `sonarqube-jenkins-setup.md` file with a clear, structured guide for setting up SonarQube integration with Jenkins:

---

```markdown
# ✅ Step-by-Step Setup: SonarQube Integration with Jenkins

This guide walks you through integrating SonarQube with Jenkins for static code analysis.

---

## 🔧 1. Install & Run SonarQube Server (Locally using Docker)

If you don’t have a running SonarQube server, here’s a quick Docker-based setup:

```bash
docker run -d --name sonarqube \
  -p 9000:9000 \
  -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true \
  sonarqube:community
```

- Access it at: [http://localhost:9000](http://localhost:9000)

**Default credentials:**

- Username: `admin`  
- Password: `admin`

> 👉 Change the password on first login.

---

## 🔐 2. Create a SonarQube Token

1. Login to SonarQube.
2. Go to **My Account → Security**.
3. Enter a name (e.g., `jenkins-token`) and click **Generate**.
4. **Copy and save the token** — you'll need it in Jenkins.

---

## 🔌 3. Install SonarQube Scanner Plugin in Jenkins

1. Go to **Manage Jenkins → Plugins**.
2. Under the **Available** tab, search for:
   - `SonarQube Scanner for Jenkins`
3. Install it and restart Jenkins if required.

---

## 🧾 4. Add SonarQube Server in Jenkins

1. Go to **Manage Jenkins → Configure System**.
2. Scroll to **SonarQube servers**.
3. Click **Add SonarQube** and fill in the details:
   - **Name**: `SonarQube` (must match what's used in the pipeline)
   - **Server URL**: `http://localhost:9000`
4. For **Server Authentication Token**:
   - Click **Add → Jenkins**
   - Kind: `Secret text`
   - Scope: `Global`
   - Secret: _Paste the SonarQube token you created_
   - ID: `sonarqube-token`
5. Select the credentials from the dropdown.
6. Click **Save**.

---

## ⚙️ 5. Configure SonarQube Scanner in Jenkins

1. Go to **Manage Jenkins → Global Tool Configuration**.
2. Find **SonarQube Scanner**.
3. Click **Add SonarQube Scanner**.
4. Name it: `SonarScanner`.
5. Check **Install automatically**.
6. Click **Save**.

---

## 🔐 6. Add SonarQube Token to Jenkins Credentials (If not done in Step 4)

1. Go to **Manage Jenkins → Credentials → Global**.
2. Click **Add Credentials**.
3. Choose:
   - Kind: `Secret text`
   - Secret: _Paste your SonarQube token_
   - ID: `sonarqube-token`
   - Description: `SonarQube token for Jenkins`

---

## ✅ You’re Ready to Use SonarQube in Your Pipeline!

### Example usage in a `Jenkinsfile`:

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

Replace `my-project` with your actual SonarQube project key.

---

## 📚 References

- [SonarQube Documentation](https://docs.sonarsource.com/)
- [Jenkins Plugin Site - SonarQube Scanner](https://plugins.jenkins.io/sonar/)
```

---

