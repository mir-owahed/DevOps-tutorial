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
Install Dependency-Check
```
$ VERSION=$(curl -s https://jeremylong.github.io/DependencyCheck/current.txt)
$ curl -Ls "https://github.com/jeremylong/DependencyCheck/releases/download/v$VERSION/dependency-check-$VERSION-release.zip" --output dependency-check.zip
```

