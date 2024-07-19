Install Nexus
```
docker run -d -p 8081:8081 --name nexus sonatype/nexus3
```
Install Sonarqube
```
docker run -d -p 9000:9000 sonarqube:lts-community
```
