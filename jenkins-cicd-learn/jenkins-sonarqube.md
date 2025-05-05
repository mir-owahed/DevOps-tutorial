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
### Configure a Sonar Server locally

```
apt install unzip
adduser sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
unzip *
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
./sonar.sh start
```

Hurray !! Now you can access the `SonarQube Server` on `http://<ip-address>:9000` 



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
pipeline directly on the Jenkins host (no Docker) using an agent label (e.g., linux) and sonarqube runs on the same host. 
```
pipeline {
    agent { label 'linux' }

    environment {
        SONAR_URL = 'http://localhost:9000'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    changelog: false, 
                    poll: false, 
                    url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('SonarQube Code Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonarqube-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        mvn clean verify sonar:sonar \
                          -Dsonar.projectKey=boardgame-app \
                          -Dsonar.host.url=$SONAR_URL \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
                }
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
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        SONAR_URL = "http://34.201.116.83:9000"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/mir-owahed/Boardgame.git'
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

        
    }
}
```

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



Here’s the **step-by-step blog post** in markdown format for integrating SonarQube with Jenkins, assuming you've already installed the **SonarQube Scanner Plugin** through the Jenkins UI:


# Jenkins Pipeline for SonarQube Integration: Code Analysis with Maven

In this blog post, we will walk through the steps to create a Jenkins pipeline that integrates **SonarQube** for code quality analysis, using **Maven** as the build tool. The pipeline will analyze the code on **SonarQube** and provide feedback on quality metrics like bugs, vulnerabilities, and code coverage.

## Prerequisites

Before starting, ensure the following:
- **Jenkins** is installed and running.
- **SonarQube** is installed and running on your system (`http://localhost:9000` or your configured server).
- **SonarQube Scanner Plugin** is installed in Jenkins through the **Jenkins UI**.
- A **SonarQube token** is generated for authentication.

## Step 1: Set Up Jenkins with SonarQube Plugin

### 1.1. Install the SonarQube Scanner Plugin

- Navigate to **Manage Jenkins → Manage Plugins**.
- Search for **SonarQube Scanner Plugin** and install it if not already installed.

### 1.2. Configure SonarQube in Jenkins

1. Go to **Manage Jenkins → Configure System**.
2. Scroll down to the **SonarQube Servers** section.
3. Click **Add SonarQube**.
4. In the **Name** field, enter `SonarQube`.
5. Set the **Server URL** to `http://localhost:9000` (or your SonarQube server).
6. In the **Server Authentication Token** field, add your SonarQube token.
7. Save the configuration.

---

## Step 2: Create the Pipeline in Jenkins

### 2.1. Navigate to Jenkins Dashboard

- Go to **Jenkins Dashboard** and click on **New Item**.
- Select **Pipeline** and give it a name (e.g., `sonarqube-pipeline`).

### 2.2. Set Up the Pipeline

In the **Pipeline** section, paste the following code:

```groovy
pipeline {
    agent { label 'linux' }

    environment {
        SONAR_URL = 'http://localhost:9000'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    changelog: false, 
                    poll: false, 
                    url: 'https://github.com/mir-owahed/Boardgame.git'
            }
        }

        stage('SonarQube Code Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        mvn clean verify sonar:sonar \
                          -Dsonar.projectKey=boardgame-app \
                          -Dsonar.host.url=$SONAR_URL \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}
````

### 2.3. Explanation of the Pipeline

* **`agent { label 'linux' }`**: Specifies that the pipeline will run on a node labeled `linux`.
* **`environment { SONAR_URL = 'http://localhost:9000' }`**: Sets the environment variable for SonarQube URL.
* **`stages { ... }`**: Defines the stages in the pipeline.

  * **Checkout Stage**: Fetches the latest code from your GitHub repository.
  * **SonarQube Code Analysis Stage**: Runs the **SonarQube analysis** using Maven and the **SonarQube token** for authentication.

---

## Step 3: Configure Jenkins with SonarQube Token

### 3.1. Generate a SonarQube Token

1. Log in to your **SonarQube** instance.
2. Go to **My Account → Security**.
3. Generate a new token and copy it.

### 3.2. Add the Token in Jenkins Credentials

1. In **Jenkins**, go to **Manage Jenkins → Manage Credentials**.
2. Select the appropriate **Jenkins store**.
3. Click **Add Credentials** and choose **Secret text**.
4. Paste your SonarQube token in the **Secret** field and give it an ID like `sonarqube-token`.

---

## Step 4: Run the Pipeline

Once the pipeline is configured, you can trigger it manually or via a **GitHub webhook**.

### 4.1. Trigger the Pipeline

* Click on **Build Now** in Jenkins to start the pipeline.
* It will:

  * **Checkout** the code from the GitHub repository.
  * **Run the SonarQube analysis** using Maven.

### 4.2. View the Results

* After the pipeline completes, you can view the SonarQube analysis results on your SonarQube dashboard.

---

## Conclusion

In this tutorial, we created a simple Jenkins pipeline that integrates with **SonarQube** for code quality analysis using **Maven**. This setup ensures that every time you commit code, Jenkins runs a SonarQube scan and provides detailed analysis on the quality of the code.

Feel free to extend this pipeline by adding stages for unit tests, building artifacts, or deploying the application.

---

### References:

* [SonarQube Documentation](https://docs.sonarqube.org/latest/)
* [Jenkins Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/)

---



