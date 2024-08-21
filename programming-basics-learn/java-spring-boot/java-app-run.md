Run java based app on VM 
1.  Identify any java based app from Github repo
```
git clone https://github.com/spring-projects/spring-petclinic.git
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
java -jar name-of-the-jar
```
4.  access the app
```
http://localhost:8080
or
curl http://localhost:8080
```
