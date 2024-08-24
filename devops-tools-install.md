### Docker Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```


Install Nexus
```
docker run -d -p 8081:8081 --name nexus sonatype/nexus3
```
Install Sonarqube
```
docker run -d -p 9000:9000 sonarqube:lts-community
```
Install trivy on ubuntu
```
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```
Trivy File System Scan
```sh
trivy fs --format table -o trivy-fs-report.html .
```
Trivy Docker Image Scan
```
trivy image --format table -o trivy-image-report.html ganeshperumal007/boardshack:latest
```



Install OWASP Dependency-Check

[Reference]

1. <https://github.com/jeremylong/DependencyCheck>

2. <https://jeremylong.github.io/DependencyCheck/>
```
$ VERSION=$(curl -s https://jeremylong.github.io/DependencyCheck/current.txt)
$ curl -Ls "https://github.com/jeremylong/DependencyCheck/releases/download/v$VERSION/dependency-check-$VERSION-release.zip" --output dependency-check.zip
```
## Install sonarqube on ubuntu

### Create an EC2 instance:
   -  Create an EC2 instance on AWS.
   -  Install GitLab Runner on the EC2 instance.
   -  Register the runner with your GitLab instance.
   -  Install Java (openjdk-11-jre)
   -  Install Docker
   -  Install SonarQube and configure it to run on http://<ip>:9000 [Don't worry detailed steps are provided].
   -  Open the Inbound ports - 80, 443 and 9000
   -  Open the Outbound ports - 80 and 443

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

...........................
<https://medium.com/@sejalmaniyar9/building-a-continuous-integration-pipeline-with-gitlab-maven-and-sonarqube-on-aws-474e4df07913>
Generating a SonarQube Authentication Token

To secure the interaction between your GitLab CI/CD pipeline and SonarQube, you’ll need to generate an authentication token in SonarQube and configure it in your CI/CD environment variables. This token will allow the pipeline to communicate with SonarQube securely.

Follow these steps to generate a SonarQube authentication token:

    - Log in to SonarQube: Access your SonarQube web interface by navigating to http://your-ec2-public-ip:9000 in your web browser. Log in using your SonarQube administrator credentials.
    
    - Navigate to User Settings: Click on your profile picture or username in the top-right corner of the SonarQube interface, and select “My Account” from the dropdown menu.
    
    - Generate Token: In the user settings page, click on the “Security” tab. Here, you will find an option to generate a token. Click on the “Generate” button.
    
    - Provide Token Name: Give your token a meaningful name that will help you identify its purpose. For example, you can name it “GitLab CI/CD Token.”
    
    - Copy the Token: Once generated, a token will be displayed on the screen. This token is crucial for authenticating your GitLab CI/CD pipeline with SonarQube. Copy the token and keep it secure as it will not be displayed again.
    
    - Configure GitLab CI/CD Variables: Return to your GitLab project’s settings and navigate to Settings > CI/CD > Variables.
    
    - Add a New Variable: Create a new variable with the name SONAR_LOGIN and paste the token you generated from SonarQube as the variable’s value.
    
    - Save Variables: Click on the “Add Variable” button to save the SONAR_LOGIN variable.

Now, your GitLab CI/CD pipeline is configured to use this authentication token when interacting with SonarQube. This token ensures that only authorized access is granted to SonarQube for code analysis and other operations, enhancing the security of your CI/CD process.

With the SonarQube authentication token in place, your CI/CD pipeline can seamlessly integrate with SonarQube to analyze your code for quality and security without compromising on security.

