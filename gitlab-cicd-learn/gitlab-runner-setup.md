# Ultimate CICD Pipeline using GitLab

## Breif Overview 

### Create an EC2 instance:
   -  Create an EC2 instance on AWS.
   -  Install GitLab Runner on the EC2 instance.
   -  Register the runner with your GitLab instance.
   -  Install Java (openjdk-11-jre)
   -  Install Docker
   -  Install SonarQube and configure it to run on http://<ip>:9000 [Don't worry detailed steps are provided].
   -  Open the Inbound ports - 80, 443 and 9000
   -  Open the Outbound ports - 80 and 443

### Configure GitLab CI/CD Pipeline:
   - Create a new GitLab repository for your Java application [You can use the sprint-boot provided in the repo]
   -  Add a `.gitlab-ci.yml` file to the root of your repository.
   -  The `.gitlab-ci.yml` file should define the steps of the pipeline.
   -  The first step should be to build the Java application using Maven. 
   -  The second step should be to run SonarQube analysis on the code. 
   -  The third step should be to build a Docker image of the application.
   -  The fourth step should be to push the Docker image to a Docker registry.
   -  The final step should be to deploy the Docker image to Kubernetes using Argo CD. 

### Configure Argo CD:
   -  Install Argo CD on your Kubernetes cluster [I would recommend to use the Argo CD Operator]
   -  Create a new application in Argo CD to deploy your Java application.
   -  Configure the application to pull the Docker image from the Docker registry.
   -  Configure the application to use Kubernetes manifests to deploy the application.

### Test and Deploy:
   - Push your code changes to GitLab to trigger the pipeline.
   -  The pipeline will automatically build, test, and deploy your Java application to Kubernetes using Argo CD.
   -  Monitor the pipeline logs and Argo CD to ensure that the deployment is successful.

## AWS EC2 Instance Configuration

- Go to AWS Console
- Instances(running)
- Launch instances

### Install Java.

Run the below commands to install Java

Install Java

```
sudo apt update
sudo apt install openjdk-11-jre
```

Verify Java is Installed

```
java -version
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

**Note: ** By default, SonarQube will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 9000 in the inbound traffic rules as show below.

- EC2 > Instances > Click on <Instance-ID>
- In the bottom tabs -> Click on Security
- Security groups
- Add inbound traffic rules as shown in the image (you can just allow TCP 9000 as well, in my case, I allowed `All traffic`).

Hurray !! Now you can access the `SonarQube Server` on `http://<ip-address>:9000` 


## Docker Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```

All the required configuration is setup !!!





Reference:
2. <https://gitlab.com/iam-veeramalla/Jenkins-Zero-To-Hero>
1. <https://gitlab.com/mir-owahed/springboot-java-app/-/settings/ci_cd>


