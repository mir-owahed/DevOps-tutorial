Run java based app in your local machine
```
1  sudo apt update
    2  git --version
    3  git clone https://gitlab.com/mir-owahed/Boardgame.git
    4  cd Boardgame/
    5  ls
    6  java
    7  sudo apt install openjdk-17-jre-headless
    8  java --version
    9  ls
   10  mvn package
   11  ls
   12  java -jar target/database_service_project-0.0.4.jar 
   13  mvn test
   14  sudo apt install docker.io
   15  sudo chmod -aG docker $USER
   16  sudo usermod -aG docker $USER
   17  docker --version
   18  docker build -t demo-java-app:0.0.1 .
   19  ls
   20  cd Boardgame/
   21  docker build -t demo-java-app:0.0.1 .
   22  ls
   23  docker images
   24  docker run -d -p 8080:8080 demo-java-app:0.0.1
   25  history
   26  exit
   27  mvn
   28  sudo apt install maven
   29  mvn --version
   30  free -h
   31  ls
   32  cd Boardgame/
   33  ls
   34  nano Dockerfile 
   35  docker --version
   36  ls
   37  docker build -t demo-java-app:0.0.1 .
   38  sudo usermod -aG docker $USER
   39  docker build -t demo-java-app:0.0.1 .
   40  history
```
