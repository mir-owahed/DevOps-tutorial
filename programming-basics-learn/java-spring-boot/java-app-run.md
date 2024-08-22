## Run java based app on VM 
### Prerequisites

The following items should be installed in your system:

- Java 17 or newer (full JDK, not a JRE)
- Maven
1.  Identify any java based app from Github repo and 
clone it using Git:
```
git clone https://github.com/mir-owahed/spring-petclinic.git
or
git clone https://github.com/mir-owahed/Boardgame.git
or
git clone https://github.com/spring-guides/gs-spring-boot.git
or
git clone https://github.com/mir-owahed/Task-Master-Pro.git
```
2.  Build the app
```
mvn validate
mvn compile
mvn test
mvn package
```
3.  Run the Application
```
java -jar target/*.jar
```
4.  You can then access the app Visit [http://localhost:8080](http://localhost:8080) in your browser.
```
curl http://localhost:8080
```
