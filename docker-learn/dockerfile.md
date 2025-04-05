# Multi-Stage Dockerfile (Alpine + Maven + Non-Root)
## multi-stage Dockerfile for a Java Maven app using Alpine Linux and a non-root user in the final image. 
```
# Stage 1: Build stage using Maven
FROM maven:3.8.3-openjdk-17-slim AS builder

WORKDIR /app

# Copy only pom.xml and fetch dependencies first (for caching)
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy rest of the app source
COPY src ./src

# Build the application
RUN mvn package -DskipTests

# Stage 2: Runtime stage using Alpine and non-root user
FROM eclipse-temurin:17-jre-alpine

# Create app directory
WORKDIR /app

# Create non-root user and group
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Copy the built JAR from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Change ownership and switch to non-root user
RUN chown -R appuser:appgroup /app
USER appuser

# Expose app port
EXPOSE 8080

# Run the app
ENTRYPOINT ["java", "-jar", "app.jar"]
```

## production-ready multi-stage Dockerfile for a Java Gradle application using an Alpine-based OpenJDK image and a non-root user
## Dockerfile for a Java Gradle application using build.gradle (Groovy DSL), with a production-ready multi-stage setup using an Alpine-based image and non-root user:
## Dockerfile for Java + Gradle (Groovy)
```
# Stage 1: Build stage using Gradle with JDK 17
FROM gradle:8.5-jdk17-alpine AS builder

# Set working directory
WORKDIR /app

# Copy Gradle wrapper and build config files first to cache dependencies
COPY build.gradle settings.gradle gradle.properties ./
COPY gradle ./gradle

# Pre-download dependencies
RUN gradle build --no-daemon || return 0

# Copy the rest of the source code
COPY . .

# Build the application
RUN gradle clean build --no-daemon

# Stage 2: Lightweight runtime image
FROM eclipse-temurin:17-jre-alpine

# Create a non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

WORKDIR /app

# Copy the built JAR file
COPY --from=builder /app/build/libs/*.jar app.jar

# Expose the app port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
```
## .dockerignore
```
.gradle
build
out
.idea/
*.iml
*.log
*.env
*.pem
```
