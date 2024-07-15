## Write 1st code on java spring-boot or

## Write hello world program on java

## Easy way- 
1. open [﻿start.spring.io/](https://start.spring.io/) 
2. open [﻿spring.io/guides/gs/spring-boot](https://spring.io/guides/gs/spring-boot) 
3. open [﻿maven.apache.org/guides/getting-started/maven-in-five-minutes.html](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) 

## Structure of java spring-boot app
- src folder
- POM file - dependencies are mentioned here

## steps: 
  - Write
  - Build
  - Run 

## what is build in SW
- It converts code into machine readable/ binaries/ executable/ jar /war
- java - compiled language
- maven - build tool for java based app
  ![image](https://github.com/mir-owahed/DevOps-tutorial/assets/133110800/86713b92-45dd-4d0d-b2bd-ec27581c5ee6)


## Prerequisite:
- install java jdk not jre on machine
- install maven

## commands:
```
sudo apt update
sudo apt install openjdk-17-jdk
sudo apt install maven
java --version
javac --version
mvn --version

mvn compile
mvn test
mvn package [It creates target folder and it contains jar or war file]
mvn clean package
```
Run app
```
java -jar name of the jar
```

Maven Command Examples:

Here are some common Maven commands:
```
    mvn compile: Compiles the project's source code.
    mvn test: Runs unit tests against compiled code.
    mvn package: Packages the compiled code into a distributable format.
    mvn install: Installs the package into the local repository.
    mvn deploy: Deploys the package to a remote repository.
    mvn site: Generates project documentation and reports.
    mvn site-deploy: Deploys the generated documentation to a remote web server.
    mvn clean: Executes the clean phase, deleting any previous build outputs.
```

## Default port for java app 8080 and can change at `application.properties` file
server.port=9000
curl http://localhost:8080
## or open browser 'http://localhost:8080'
