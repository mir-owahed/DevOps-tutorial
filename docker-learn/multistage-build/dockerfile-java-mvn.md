```
# ---------- Stage 1: Build the Spring Boot App ----------
FROM maven:3.8.7-eclipse-temurin-17 AS builder

# Set working directory
WORKDIR /app

# Copy pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy source code
COPY src ./src

# Build the JAR file
RUN mvn clean package -DskipTests

# ---------- Stage 2: Create Lightweight Image ----------
FROM eclipse-temurin:17-jdk-alpine

# Create a non-root user
RUN addgroup -S spring && adduser -S spring -G spring

# Set work directory
WORKDIR /app

# Copy the JAR file from builder stage
COPY --from=builder /app/target/*.jar app.jar

# Set permissions
RUN chown -R spring:spring /app

# Switch to non-root user
USER spring

# Expose port (default Spring Boot port)
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]

```
```
# Maven artifacts
target/

# IDEs and editors
.idea/
*.iml
*.sw?

# System files
.DS_Store
Thumbs.db

# Logs
*.log

# Git
.git
.gitignore

# OS metadata
ehthumbs.db
desktop.ini

```
```
# Maven
target/
*.log

# IDEs
.idea/
*.iml
*.class

# OS files
.DS_Store
Thumbs.db

# Environment
.env
*.jar
*.war

```
