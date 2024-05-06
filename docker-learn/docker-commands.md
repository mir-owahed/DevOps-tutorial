# Docker commands
```
# https://docs.docker.com/build/building/multi-platform/
docker build -t python-sample-app:latest .
docker images

# Push to repository
docker login
docker tag hello-app:latest owahed1/python-sample-app:latest
docker push owahed1/python-sample-app:latest

# Pull from repository
docker pull owahed1/python-sample-app:latest
docker images

# Run container
docker run --rm -d -p 5000:5000 owahed1/python-sample-app:latest
docker ps

# Analyse container
docker inspect <ID> | vim -
docker logs -f <ID>
docker exec -it <ID> /bin/ls -al
docker exec -it <ID> /bin/bash

# Remove image, Build again, with versioning
docker rmi <ID>
docker build -t owahed1/python-sample-app:latest .

# Stop & destroy
docker stop <ID>
docker rm <ID>
```

