# Docker Hands-On Tutorial - Detailed Beginner Explanation

## 1. Video Introduction
The tutorial explains Docker container fundamentals with hands-on commands.

## 2. What is a Container?
- A container packages an app with its dependencies.
- Runs consistently across environments.
- Only Docker runtime required on host.

## 3. Prerequisite
- Docker installed on host (Ubuntu VM used in transcript).

## 4. Virtual Machine Setup
- Docker installed inside Ubuntu VM on Windows using VirtualBox.

## 5. Docker Installation (Ubuntu)
- Check: `docker --version`
- Install from official Docker repository using apt.
- Resolve permission denial using `sudo usermod -aG docker $USER`.

## 6. Test Docker
```bash
docker run hello-world
```

## 7. VM vs Container
- VM is heavy; container is lightweight and shares host kernel.

## 8. Docker Lifecycle
1. Write app
2. Create Dockerfile
3. Build image
4. Run container

## 9. Example App
- Go API cloned using `git clone`.

## 10. Dockerfile Explanation
- `FROM` = base image
- `WORKDIR` = working directory
- `ADD`/`COPY` = add source
- `RUN` = build
- `EXPOSE` = container port
- `CMD` = startup command

## 11. Build Image
```bash
docker build -t go-app:V1 .
docker images
```

## 12. Run Container with Ports
```bash
docker run -d -p 8080:8000 go-app:V1
```

## 13. Manage Containers
```bash
docker ps
docker ps -a
docker stop <id>
docker rm <id>
```

## 14. Delete Image
```bash
docker rmi <image-id>
```

## 15. Inspect & Logs
```bash
docker inspect <id>
docker logs <id>
```

## 16. Enter Container
```bash
docker exec -it <id> /bin/sh
```

## 17. Push to Docker Hub
```bash
docker tag go-app:V1 username/go-app:V1
docker login
docker push username/go-app:V1
```

## 18. Pull Image
```bash
docker pull username/go-app:V1
```

## 19. Cleanup
```bash
docker system prune -a
```

## 20. Cheat Sheet
```bash
docker --version
docker run hello-world
docker build -t name .
docker run -d -p host:container name
docker ps -a
docker stop <id>
docker rm <id>
docker rmi <id>
docker exec -it <id> /bin/sh
docker tag old new
docker login
docker push
docker pull
```
