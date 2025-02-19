# Docker commands
```
@mir-owahed ➜ ~ $ docker ps -a
CONTAINER ID   IMAGE                COMMAND               CREATED      STATUS                  PORTS     NAMES
2f53ded79854   product-catalog:v1   "./product-catalog"   2 days ago   Exited (1) 2 days ago             serene_curie
32195d1a70d2   product-catalog:v1   "./product-catalog"   2 days ago   Exited (1) 2 days ago             amazing_liskov
bb8317d42100   d471189fcded         "./product-catalog"   2 days ago   Exited (1) 2 days ago             cranky_torvalds
bda2bdd817fe   product-catalog:v1   "./product-catalog"   2 days ago   Exited (1) 2 days ago             upbeat_matsumoto
a4d7f80d510a   product-catalog:v1   "./product-catalog"   2 days ago   Exited (1) 2 days ago             affectionate_williamson
@mir-owahed ➜ ~ $ docker system prune -a
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all images without at least one container associated to them
  - all build cache

Are you sure you want to continue? [y/N] y
Deleted Containers:
2f53ded798549531b37d52b4465667b4729b19d0e3032be5d9ee4071602e12a7
32195d1a70d2bb3727b781a4982b825254aaf53ec8bd6a95ee36e9971e81fa7b
bb8317d42100a370ab41978a49c364401173c6c9ef921936e6f5ed96a9efd774
bda2bdd817fedce00ec6b9d0bb3fd1cf276a4a8446dfaeb2690f17d7a80f33f8
a4d7f80d510a9e1438244a714f9e7770ba11cbf2a2bc3978a5f09527b2bf7607

Deleted Images:
untagged: product-catalog:v1
deleted: sha256:d471189fcded7dc5bc069258dde37201700b128fd3fe9677933dc0dd6188ae56

Deleted build cache objects:
9179iywo9y4ds1ydtddlvpgii
7t1gqg8a11tv4t61xifwl0jz3
r9c531mpm7w0i71akgaj4grhq
o1cvlclwadw37s2a8eyv3ad8q
lz12h3c9orhhvwl1aqwquda9y
kr5jcyx3nsrow61vazo8veccw
v71py4i5u9oq5w9cdsljih310
q9oevpuy26lyyvt1mg6qlhatp
jjzuwty0xh9wnn20ixc513ars
ua50j3u4yv5jiv1pna1hbmft4
r51u4kpsq9sur96dsq96irzoe
q4f1o1df2vbpe7iv1f91hdec1
xyn3gf57qpm71gddm8hmczn4l
s4fpp6kjdso3if7kdpfii5xov
qmm0w6cnudmbc17n6fyvanh05
xsc2r75xx2s9sxee12va297gq
8commbnmwqtedoe777npdotrr
r1zbx8zen473bx3bscezuikgf
iy1h9qcfo4j4p5yilr2v7nafa

Total reclaimed space: 1GB

@mir-owahed ➜ ~ $ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
e6590344b1a5: Pull complete 
Digest: sha256:e0b569a5163a5e6be84e210a2587e7d447e08f87a0e90798363fa44a0464a1e8
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

@mir-owahed ➜ ~ $ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
bfc918c091a5   hello-world   "/hello"   2 minutes ago   Exited (0) 2 minutes ago             vigilant_herschel
@mir-owahed ➜ ~ $ sudo usermod -aG docker $USER


```
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
docker run --rm -p 5000:5000 owahed1/python-sample-app:latest
docker run -d -p 5000:5000 owahed1/python-sample-app:latest
docker ps
docker ps -a

# Analyse container
docker inspect <ID> | vim -
docker logs -f <ID>
docker logs <ID>
docker exec -it <ID> /bin/ls -al
docker exec -it <ID> /bin/bash
docker exec <ID> pwd
docker exec <ID> ls -la

# Remove image, Build again, with versioning
docker rmi <ID>
docker build -t owahed1/python-sample-app:latest .

# Stop & destroy
docker stop <ID>
docker rm <ID>
docker ps -aq | xargs docker stop | xargs docker rm

# docker manual
docker --help
docker command --help
docker logs --help
```


