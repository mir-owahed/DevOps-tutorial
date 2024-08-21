Run java based app on VM 
### Prerequisites

The following items should be installed in your system:

- Java 17 or newer (full JDK, not a JRE)
- Maven
1.  Identify any java based app from Github repo

```
https://github.com/mir-owahed/spring-petclinic.git
or
git clone https://github.com/mir-owahed/Boardgame
```
2.  Build the app
```
mvn validate
mvn compile
mvn test
mvn package
```
3.  Run app using package
```
java -jar target/*.jar
```
4.  You can then access the app at <http://localhost:8080/>
```
curl http://localhost:8080
```
