Prerequisites

    Install Java Development Kit (JDK)

```
sudo apt update
sudo apt install openjdk-11-jdk -y
```
Verify the installation:
```
java -version
```
Install Maven
```

sudo apt install maven -y
```
Verify the Maven installation:

```bash

mvn -version
```
Install Git

```bash

    sudo apt install git -y
```
Steps to Clone, Build, Test, and Run the Application
1. Clone the GitLab Repository

    Clone the repository to your local machine:

    ```bash

git clone https://gitlab.com/mir-owahed/Boardgame.git
```
Navigate to the cloned project directory:

```bash

    cd Boardgame
```
2. Understand the Project Structure

    The project will have a structure similar to:

    
```
    Boardgame/
    ├── pom.xml
    └── src
        ├── main
        │   └── java
        │       └── <package_structure>
        └── test
            └── java
                └── <test_package_structure>

    The pom.xml file is crucial as it contains the project configuration, dependencies, and build settings.
```
3. Build the Project

    Compile the project using Maven:

    ```bash

    mvn compile
```
4. Run the Tests

    Execute the unit tests provided in the project:

    ```bash

    mvn test
```
5. Package the Application

    Package the project into a JAR file:

    ```bash

    mvn package
```
    The JAR file will be located in the target directory.

6. Run the Application

    To run the application, use the following command:

    ```bash

    java -jar target/*.jar
```
    This command will execute the JAR file that was generated during the packaging step.

Summary of Commands

```bash

sudo apt update
sudo apt install openjdk-11-jdk maven git -y
git clone https://gitlab.com/mir-owahed/Boardgame.git
cd Boardgame
mvn compile
mvn test
mvn package
java -jar target/*.jar
```
Conclusion

By following these steps, you can clone, build, test, and run the Java-based application from the GitLab repository using Maven on an Ubuntu system. The java -jar target/*.jar command is a simple and effective way to run the packaged application.
