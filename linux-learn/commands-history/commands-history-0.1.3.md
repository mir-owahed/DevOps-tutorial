```
docker --version
docker images
docker images fda1f6976755
docker images 
docker rmi fda1f6976755
docker rmi 98ca9b5cd278
docker ps
docker ps -a
docker stop 78dfbbb366b9
docker stop 4dcc61c6b62e
docker images
docker rmi 98ca9b5cd278
docker images
docker ps -a
docker rm 78dfbbb366b9
docker rm 4dcc61c6b62e
docker images
docker rmi 98ca9b5cd278
ls
docker build -t python-hello-app .
docker images
docker tag --help
docker tag python-hello-app:latest owahed1/python-sample-app:0.0.1
docker images
docker rmi 7c92261ad4fa
docker rmi -f 7c92261ad4fa
docker login
docker push owahed1/python-sample-app:0.0.1
docker images
docker build -t python-hello-app .
docker tag python-hello-app:latest owahed1/python-sample-app:0.0.1
docker images
docker push owahed1/python-sample-app:0.0.1
docker images
docker rmi owahed1/python-sample-app:0.0.1
docker images
docker rmi python-hello-app:latest
docker images
clear
docker pull owahed1/python-sample-app:0.0.1
docker images
ls
cat app.py 
ddocker run -p 8000:5000 owahed1/python-sample-app:0.0.1
docker run -p 8000:5000 owahed1/python-sample-app:0.0.1
exit
history
docker ps
docker ps -a
docker run -p -d 8000:5000 owahed1/python-sample-app:0.0.1
docker run -d -p 8000:5000 owahed1/python-sample-app:0.0.1
docker ps
docker rm f4e58d9e0915
docker stop f4e58d9e0915
docker rm f4e58d9e0915
docker ps
docker ps -a
docker run --rm -d -p 8001:5000 owahed1/python-sample-app:0.0.1
curl http://localhost:8001/
curl http://localhost:8001/ping
docker ps
docker stop 4f63990a881f
docker ps
docker run --rm -d -p 8001:5000 owahed1/python-sample-app:0.0.1
docker ps
docker exec -it a27c86738456 bash
docker exec -it a27c86738456 ls -la
docker exec -it a27c86738456 pwd
docker exec -it a27c86738456 /bin/bash
docker logs a27c86738456
docker logs -f a27c86738456
history
```
