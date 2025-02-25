# Docker commands
```
@mir-owahed ➜ /workspaces/go-lang-app (main) $ history 
    1  docker version
    2  ls
    3  docker ps
    4  docker images
    5  docker ps -a
    6  docker build -t go-app:v1 .
    7  docker images
    8  docker run -d -p 8080:8000 go-app:v1
    9  docker ps
   10  docker ps -a
   11  docker images
   12  docker stop a75c3e430c95
   13  docker ps
   14  docker ps -a
   15  docker rmi 378513c83eaf
   16  docker rm a75c3e430c95
   17  docker ps -a
   18  docker rmi 378513c83eaf
   19  docker images
   20  docker build -t go-app:v1 -f dockerfile.multi .
   21  docker images
   22  docker tag go-app:v1 owahed1/demo-app:go-app-v1
   23  docker images
   24  docker rmi go-app:v1
   25  docker images
   26  docker login -u owahed1
   27  docker push owahed1/demo-app:go-app-v1
   28  docker login -u owahed1
   29  docker push owahed1/demo-app:go-app-v1
   30  docker images
   31  docker rmi b1bab61ef405
   32  docker images
   33  docker pull owahed1/demo-app:go-app-v1
   34  docker run -d -p 8000:8000 owahed1/demo-app:go-app-v1
   35  docker ps
   36  docker exec ed8e8ee93c60 pwd
   37  docker exec -it ed8e8ee93c60 pwd
   38  docker exec -it ed8e8ee93c60 ls -la
   39  docker exec -it ed8e8ee93c60 /bash
   40  docker inspect ed8e8ee93c60 | vim -
   41  docker logs ed8e8ee93c60
   42  history
................................................
@mir-owahed ➜ /workspaces/codespaces-blank $ history
    1  history
    2  ls
    3  docker ps -a
    4  docker system prune -a
    5  docker ps -a
    6  history
    7  docker images
    8  docker pull alpine
    9  docker images
   10  docker ps
   11  docker run -d -t --name server alpine
   12  docker ps
   13  docker exec -it d108148f4e56 ls -la
   14  docker exec -it sh
   15  docker exec -it d108148f4e56 sh
   16  history
   17  docker ps -a
   18  docker exec -it d108148f4e56 /bin/bash
   19  docker exec -it d108148f4e56 /bin/sh
   20  docker ps -a
   21  docker ps
   22  docker stop d108148f4e56
   23  docker ps
   24  docker ps -a
   25  docker rm d108148f4e56
   26  docker ps -a
   27  docker images
   28  docker rmi aded1e1a5b37
   29  hisory
   30  history
```
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
docker exec -it <ID> sh
docker exec -it <ID> /bin/ls -al
docker exec -it <ID> /bin/bash
docker exec -it <ID> pwd
docker exec -it <ID> ls -la

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
```
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker version
Client:
 Version:           27.3.1-1
 API version:       1.47
 Go version:        go1.22.8
 Git commit:        ce1223035ac3ab8922717092e63a184cf67b493d
 Built:             Fri Sep 20 11:01:47 UTC 2024
 OS/Arch:           linux/amd64
 Context:           default

Server:
 Engine:
  Version:          27.3.1-1
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.22.8
  Git commit:       41ca978a0a5400cc24b274137efa9f25517fcc0b
  Built:            Wed Sep 18 10:25:38 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.36-1
  GitCommit:        88c3d9bc5b5a193f40b7c14fa996d23532d6f956
 runc:
  Version:          1.1.15-1
  GitCommit:        bc20cb4497af9af01bea4a8044f1678ffca2745c
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
@mir-owahed ➜ /workspaces/go-lang-app (main) $ ls
Dockerfile  README.md  commands.txt  dockerfile.multi  go.mod  hello.go
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker build -t go-app:v1 .
[+] Building 31.8s (10/10) FINISHED                                                                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                                                                     0.0s
 => => transferring dockerfile: 163B                                                                                                                                     0.0s
 => [internal] load metadata for docker.io/library/golang:1.22-alpine                                                                                                    2.5s
 => [auth] library/golang:pull token for registry-1.docker.io                                                                                                            0.0s
 => [internal] load .dockerignore                                                                                                                                        0.0s
 => => transferring context: 2B                                                                                                                                          0.0s
 => [1/4] FROM docker.io/library/golang:1.22-alpine@sha256:1699c10032ca2582ec89a24a1312d986a3f094aed3d5c1147b19880afe40e052                                             10.2s
 => => resolve docker.io/library/golang:1.22-alpine@sha256:1699c10032ca2582ec89a24a1312d986a3f094aed3d5c1147b19880afe40e052                                              0.0s
 => => sha256:4129f51f28c9ae5de799b958ba2aaa8f92f26cc7bf47c107891673fe4b516c03 2.08kB / 2.08kB                                                                           0.0s
 => => sha256:1f3e46996e2966e4faa5846e56e76e3748b7315e2ded61476c24403d592134f0 3.64MB / 3.64MB                                                                           0.3s
 => => sha256:4d75fd4b73869ed224045c010cdec78756eefb6752a5a8e4804294009eac11e9 294.90kB / 294.90kB                                                                       0.4s
 => => sha256:afa154b433c7f72db064d19e1bcfa84ee196ad29120328f6bdb2c5fbd7b8eeac 69.36MB / 69.36MB                                                                         1.8s
 => => sha256:1699c10032ca2582ec89a24a1312d986a3f094aed3d5c1147b19880afe40e052 10.30kB / 10.30kB                                                                         0.0s
 => => sha256:6d405dfc5fdf3a45df1529cf060b920041f52ce523487e0f36f02765af294a51 1.92kB / 1.92kB                                                                           0.0s
 => => extracting sha256:1f3e46996e2966e4faa5846e56e76e3748b7315e2ded61476c24403d592134f0                                                                                0.1s
 => => sha256:5f837c998576dcb54bc285997f33fcc2166dff6aa48fe3a374da92474efd5fe8 126B / 126B                                                                               0.7s
 => => extracting sha256:4d75fd4b73869ed224045c010cdec78756eefb6752a5a8e4804294009eac11e9                                                                                0.0s
 => => sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1 32B / 32B                                                                                 0.8s
 => => extracting sha256:afa154b433c7f72db064d19e1bcfa84ee196ad29120328f6bdb2c5fbd7b8eeac                                                                                4.6s
 => => extracting sha256:5f837c998576dcb54bc285997f33fcc2166dff6aa48fe3a374da92474efd5fe8                                                                                0.0s
 => => extracting sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1                                                                                0.0s
 => [internal] load build context                                                                                                                                        0.0s
 => => transferring context: 60.15kB                                                                                                                                     0.0s
 => [2/4] WORKDIR /src                                                                                                                                                   0.0s
 => [3/4] ADD . .                                                                                                                                                        0.0s
 => [4/4] RUN CGO_ENABLED=0 go build -o go-lang-app .                                                                                                                   17.1s
 => exporting to image                                                                                                                                                   1.8s
 => => exporting layers                                                                                                                                                  1.8s
 => => writing image sha256:378513c83eaf2717deebf95d5874729fdba6a692e93979492e502f88cf8d29f8                                                                             0.0s
 => => naming to docker.io/library/go-app:v1                                                                                                                             0.0s
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
go-app       v1        378513c83eaf   17 seconds ago   304MB

@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker run -d -p 8080:8000 go-app:v1
a75c3e430c95f9f2ec7ef0f635b14804ddf03dd8e6fd0959f796ebd8f3613cdd
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE       COMMAND           CREATED          STATUS          PORTS                                         NAMES
a75c3e430c95   go-app:v1   "./go-lang-app"   49 seconds ago   Up 48 seconds   0.0.0.0:8080->8000/tcp, [::]:8080->8000/tcp   romantic_napier
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE       COMMAND           CREATED         STATUS         PORTS                                         NAMES
a75c3e430c95   go-app:v1   "./go-lang-app"   2 minutes ago   Up 2 minutes   0.0.0.0:8080->8000/tcp, [::]:8080->8000/tcp   romantic_napier
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
go-app       v1        378513c83eaf   6 minutes ago   304MB
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker stop a75c3e430c95
a75c3e430c95
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE       COMMAND           CREATED         STATUS                      PORTS     NAMES
a75c3e430c95   go-app:v1   "./go-lang-app"   4 minutes ago   Exited (2) 18 seconds ago             romantic_napier
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rmi 378513c83eaf
Error response from daemon: conflict: unable to delete 378513c83eaf (must be forced) - image is being used by stopped container a75c3e430c95
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rm a75c3e430c95
a75c3e430c95
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rmi 378513c83eaf
Untagged: go-app:v1
Deleted: sha256:378513c83eaf2717deebf95d5874729fdba6a692e93979492e502f88cf8d29f8
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker build -t go-app:v1 -f dockerfile.multi .
[+] Building 21.1s (14/14) FINISHED                                                                                                                            docker:default
 => [internal] load build definition from dockerfile.multi                                                                                                               0.0s
 => => transferring dockerfile: 291B                                                                                                                                     0.0s
 => [internal] load metadata for gcr.io/distroless/base-debian12:latest                                                                                                  2.2s
 => [internal] load metadata for docker.io/library/golang:1.22-alpine                                                                                                    1.4s
 => [auth] library/golang:pull token for registry-1.docker.io                                                                                                            0.0s
 => [internal] load .dockerignore                                                                                                                                        0.0s
 => => transferring context: 2B                                                                                                                                          0.0s
 => CACHED [builder 1/4] FROM docker.io/library/golang:1.22-alpine@sha256:1699c10032ca2582ec89a24a1312d986a3f094aed3d5c1147b19880afe40e052                               0.0s
 => [stage-1 1/3] FROM gcr.io/distroless/base-debian12:latest@sha256:74ddbf52d93fafbdd21b399271b0b4aac1babf8fa98cab59e5692e01169a1348                                    4.8s
 => => resolve gcr.io/distroless/base-debian12:latest@sha256:74ddbf52d93fafbdd21b399271b0b4aac1babf8fa98cab59e5692e01169a1348                                            0.0s
 => => sha256:74ddbf52d93fafbdd21b399271b0b4aac1babf8fa98cab59e5692e01169a1348 1.51kB / 1.51kB                                                                           0.0s
 => => sha256:fab58a7ef52ea73a8c91e19d80e590a03596ba016e530a9d2aad928995811633 1.71kB / 1.71kB                                                                           0.0s
 => => sha256:688513194d7a0f0d77e4a3692748d21c4ccd1af6a5ff9012f18f053ed9573c13 104.24kB / 104.24kB                                                                       1.0s
 => => sha256:ad04bf079b9ed668d38fe2138cfe575847795985097b38a400f4ef1ff69a561a 2.27kB / 2.27kB                                                                           0.0s
 => => sha256:bfb59b82a9b65e47d485e53b3e815bca3b3e21a095bd0cb88ced9ac0b48062bf 13.36kB / 13.36kB                                                                         1.0s
 => => sha256:efa9d1d5d3a286c60a7261496166fdf31cec2284dafe7eef7cda89eba2f675d6 541.99kB / 541.99kB                                                                       1.2s
 => => extracting sha256:688513194d7a0f0d77e4a3692748d21c4ccd1af6a5ff9012f18f053ed9573c13                                                                                0.0s
 => => sha256:7c12895b777bcaa8ccae0605b4de635b68fc32d60fa08f421dc3818bf55ee212 188B / 188B                                                                               1.3s
 => => extracting sha256:bfb59b82a9b65e47d485e53b3e815bca3b3e21a095bd0cb88ced9ac0b48062bf                                                                                0.0s
 => => sha256:a62778643d563b511190663ef9a77c30d46d282facfdce4f3a7aecc03423c1f3 67B / 67B                                                                                 1.4s
 => => extracting sha256:efa9d1d5d3a286c60a7261496166fdf31cec2284dafe7eef7cda89eba2f675d6                                                                                0.4s
 => => sha256:3214acf345c0cc6bbdb56b698a41ccdefc624a09d6beb0d38b5de0b2303ecaf4 123B / 123B                                                                               1.6s
 => => sha256:5664b15f108bf9436ce3312090a767300800edbbfd4511aa1a6d64357024d5dd 168B / 168B                                                                               1.7s
 => => sha256:0bab15eea81d0fe6ab56ebf5fba14e02c4c1775a7f7436fbddd3505add4e18fa 93B / 93B                                                                                 1.7s
 => => sha256:4aa0ea1413d37a58615488592a0b827ea4b2e48fa5a77cf707d0e35f025e613f 385B / 385B                                                                               2.0s
 => => sha256:da7816fa955ea24533c388143c78804c28682eef99b4ee3723b548c70148bba6 321B / 321B                                                                               2.1s
 => => sha256:9aee425378d2c16cd44177dc54a274b312897f5860a8e78fdfda555a0d79dd71 130.50kB / 130.50kB                                                                       2.7s
 => => extracting sha256:a62778643d563b511190663ef9a77c30d46d282facfdce4f3a7aecc03423c1f3                                                                                0.0s
 => => extracting sha256:7c12895b777bcaa8ccae0605b4de635b68fc32d60fa08f421dc3818bf55ee212                                                                                0.0s
 => => extracting sha256:3214acf345c0cc6bbdb56b698a41ccdefc624a09d6beb0d38b5de0b2303ecaf4                                                                                0.0s
 => => sha256:701c983262e9aa33e628c7928b9351c0c69c5e2c6b37051d2e03ad6027c5bff6 5.84MB / 5.84MB                                                                           3.7s
 => => sha256:221438ca359c95b5f7ecb07541b094ae1e5ce63442a404e8a38b6d84b6a7bcb4 2.83MB / 2.83MB                                                                           3.6s
 => => extracting sha256:5664b15f108bf9436ce3312090a767300800edbbfd4511aa1a6d64357024d5dd                                                                                0.0s
 => => extracting sha256:0bab15eea81d0fe6ab56ebf5fba14e02c4c1775a7f7436fbddd3505add4e18fa                                                                                0.0s
 => => extracting sha256:4aa0ea1413d37a58615488592a0b827ea4b2e48fa5a77cf707d0e35f025e613f                                                                                0.0s
 => => extracting sha256:da7816fa955ea24533c388143c78804c28682eef99b4ee3723b548c70148bba6                                                                                0.0s
 => => extracting sha256:9aee425378d2c16cd44177dc54a274b312897f5860a8e78fdfda555a0d79dd71                                                                                0.0s
 => => extracting sha256:701c983262e9aa33e628c7928b9351c0c69c5e2c6b37051d2e03ad6027c5bff6                                                                                0.4s
 => => extracting sha256:221438ca359c95b5f7ecb07541b094ae1e5ce63442a404e8a38b6d84b6a7bcb4                                                                                0.1s
 => [internal] load build context                                                                                                                                        0.0s
 => => transferring context: 6.21kB                                                                                                                                      0.0s
 => [builder 2/4] WORKDIR /build                                                                                                                                         0.0s
 => [builder 3/4] COPY . .                                                                                                                                               0.0s
 => [builder 4/4] RUN CGO_ENABLED=0 go build -o ./go-lang-app                                                                                                           17.8s
 => [stage-1 2/3] WORKDIR /app                                                                                                                                           0.0s
 => [stage-1 3/3] COPY --from=builder /build/go-lang-app ./go-lang-app                                                                                                   0.1s
 => exporting to image                                                                                                                                                   0.8s
 => => exporting layers                                                                                                                                                  0.8s
 => => writing image sha256:b1bab61ef405ab9c5a1aef700df721bc44bad7ff746869dad8d61bf0dc11b618                                                                             0.0s
 => => naming to docker.io/library/go-app:v1

@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
go-app       v1        b1bab61ef405   45 seconds ago   27.7MB
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker tag go-app:v1 owahed1/demo-app:go-app-v1
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY         TAG         IMAGE ID       CREATED         SIZE
go-app             v1          b1bab61ef405   2 minutes ago   27.7MB
owahed1/demo-app   go-app-v1   b1bab61ef405   2 minutes ago   27.7MB
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rmi go-app:v1
Untagged: go-app:v1
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY         TAG         IMAGE ID       CREATED         SIZE
owahed1/demo-app   go-app-v1   b1bab61ef405   2 minutes ago   27.7MB

@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker login -u owahed1
Password: 
WARNING! Your password will be stored unencrypted in /home/codespace/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credential-stores

Login Succeeded
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker push owahed1/demo-app:go-app-v1
The push refers to repository [docker.io/owahed1/demo-app]
f1ccbba4d77a: Preparing 
fe57a433df52: Preparing 
378aeea05457: Preparing 
58dd21421eb6: Preparing 
b336e209998f: Preparing 
f4aee9e53c42: Waiting 
1a73b54f556b: Waiting 
2a92d6ac9e4f: Waiting 
bbb6cacb8c82: Waiting 
6f1cdceb6a31: Waiting 
af5aa97ebe6c: Waiting 
4d049f83d9cf: Waiting 
a80545a98dcd: Waiting 
8fa10c0194df: Waiting 
f920c5680b0b: Waiting 
unauthorized: access token has insufficient scopes
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker login -u owahed1
Password: 
WARNING! Your password will be stored unencrypted in /home/codespace/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credential-stores

Login Succeeded
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker push owahed1/demo-app:go-app-v1
The push refers to repository [docker.io/owahed1/demo-app]
f1ccbba4d77a: Pushed 
fe57a433df52: Pushed 
378aeea05457: Pushed 
58dd21421eb6: Pushed 
b336e209998f: Pushed 
f4aee9e53c42: Pushed 
1a73b54f556b: Pushed 
2a92d6ac9e4f: Pushed 
bbb6cacb8c82: Pushed 
6f1cdceb6a31: Pushed 
af5aa97ebe6c: Pushed 
4d049f83d9cf: Pushed 
a80545a98dcd: Pushed 
8fa10c0194df: Pushed 
f920c5680b0b: Pushed 
go-app-v1: digest: sha256:f1ded8d2f427478c0f78ffd3219c49aeaa6ae91feab3c331e4705d87bbc80344 size: 3441

@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY         TAG         IMAGE ID       CREATED          SIZE
owahed1/demo-app   go-app-v1   b1bab61ef405   10 minutes ago   27.7MB
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rmi b1bab61ef405
Untagged: owahed1/demo-app:go-app-v1
Untagged: owahed1/demo-app@sha256:f1ded8d2f427478c0f78ffd3219c49aeaa6ae91feab3c331e4705d87bbc80344
Deleted: sha256:b1bab61ef405ab9c5a1aef700df721bc44bad7ff746869dad8d61bf0dc11b618
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker pull owahed1/demo-app:go-app-v1
go-app-v1: Pulling from owahed1/demo-app
38f4a9ccb8d6: Already exists 
2e4cf50eeb92: Already exists 
d44d440ac96b: Already exists 
0f8b424aa0b9: Already exists 
d557676654e5: Already exists 
d82bc7a76a83: Already exists 
d858cbc252ad: Already exists 
1069fc2daed1: Already exists 
b40161cd83fc: Already exists 
3f4e2c586348: Already exists 
80a8c047508a: Already exists 
68096f3f5ab9: Already exists 
04155d74e8b4: Already exists 
4037b355c923: Already exists 
7ab8644db086: Already exists 
Digest: sha256:f1ded8d2f427478c0f78ffd3219c49aeaa6ae91feab3c331e4705d87bbc80344
Status: Downloaded newer image for owahed1/demo-app:go-app-v1
docker.io/owahed1/demo-app:go-app-v1
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker run -d -p 8000:8000 owahed1/demo-app:go-app-v1
ed8e8ee93c6047a63b6b6152d7aa91ed1af67c17228a1e4ba341971860988b51
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE                        COMMAND           CREATED              STATUS              PORTS                                       NAMES
ed8e8ee93c60   owahed1/demo-app:go-app-v1   "./go-lang-app"   About a minute ago   Up About a minute   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp   zealous_cohen

@mir-owahed ➜ /workspaces/go-lang-app (main) $ 
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker exec ed8e8ee93c60 pwd
OCI runtime exec failed: exec failed: unable to start container process: exec: "pwd": executable file not found in $PATH: unknown
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker exec -it ed8e8ee93c60 pwd
OCI runtime exec failed: exec failed: unable to start container process: exec: "pwd": executable file not found in $PATH: unknown
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker exec -it ed8e8ee93c60 ls -la
OCI runtime exec failed: exec failed: unable to start container process: exec: "ls": executable file not found in $PATH: unknown
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker exec -it ed8e8ee93c60 /bash
OCI runtime exec failed: exec failed: unable to start container process: exec: "/bash": stat /bash: no such file or directory: unknown
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker inspect ed8e8ee93c60 | vim -
Vim: Reading from stdin...

@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker logs ed8e8ee93c60
Mir's server is now running
@mir-owahed ➜ /workspaces/go-lang-app (main) $

@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY         TAG         IMAGE ID       CREATED       SIZE
owahed1/demo-app   go-app-v1   b1bab61ef405   3 hours ago   27.7MB
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rmi owahed1/demo-app:go-app-v1
Error response from daemon: conflict: unable to remove repository reference "owahed1/demo-app:go-app-v1" (must force) - container ed8e8ee93c60 is using its referenced image b1bab61ef405
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE                        COMMAND           CREATED       STATUS                       PORTS                                       NAMES
ed8e8ee93c60   owahed1/demo-app:go-app-v1   "./go-lang-app"   3 hours ago   Exited (255) 4 minutes ago   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp   zealous_cohen
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rm ed8e8ee93c60
ed8e8ee93c60
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rmi owahed1/demo-app:go-app-v1
Untagged: owahed1/demo-app:go-app-v1
Untagged: owahed1/demo-app@sha256:f1ded8d2f427478c0f78ffd3219c49aeaa6ae91feab3c331e4705d87bbc80344
Deleted: sha256:b1bab61ef405ab9c5a1aef700df721bc44bad7ff746869dad8d61bf0dc11b618
@mir-owahed ➜ /workspaces/go-lang-app (main) $ ls
Dockerfile  README.md  command.txt  commands.txt  dockerfile.multi  go.mod  hello.go

@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY         TAG         IMAGE ID       CREATED       SIZE
owahed1/demo-app   go-app-v1   b1bab61ef405   3 hours ago   27.7MB
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rmi owahed1/demo-app:go-app-v1
Error response from daemon: conflict: unable to remove repository reference "owahed1/demo-app:go-app-v1" (must force) - container ed8e8ee93c60 is using its referenced image b1bab61ef405
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE                        COMMAND           CREATED       STATUS                       PORTS                                       NAMES
ed8e8ee93c60   owahed1/demo-app:go-app-v1   "./go-lang-app"   3 hours ago   Exited (255) 4 minutes ago   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp   zealous_cohen
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rm ed8e8ee93c60
ed8e8ee93c60
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker rmi owahed1/demo-app:go-app-v1
Untagged: owahed1/demo-app:go-app-v1
Untagged: owahed1/demo-app@sha256:f1ded8d2f427478c0f78ffd3219c49aeaa6ae91feab3c331e4705d87bbc80344
Deleted: sha256:b1bab61ef405ab9c5a1aef700df721bc44bad7ff746869dad8d61bf0dc11b618
@mir-owahed ➜ /workspaces/go-lang-app (main) $ ls
Dockerfile  README.md  command.txt  commands.txt  dockerfile.multi  go.mod  hello.go
@mir-owahed ➜ /workspaces/go-lang-app (main) $ ls
Dockerfile  README.md  command.txt  commands.txt  dockerfile.multi  go.mod  hello.go
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker build -t go-app:v2 .
[+] Building 21.2s (10/10) FINISHED                                                                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                                                                     0.0s
 => => transferring dockerfile: 163B                                                                                                                                     0.0s
 => [internal] load metadata for docker.io/library/golang:1.22-alpine                                                                                                    1.5s
 => [auth] library/golang:pull token for registry-1.docker.io                                                                                                            0.0s
 => [internal] load .dockerignore                                                                                                                                        0.0s
 => => transferring context: 2B                                                                                                                                          0.0s
 => [1/4] FROM docker.io/library/golang:1.22-alpine@sha256:1699c10032ca2582ec89a24a1312d986a3f094aed3d5c1147b19880afe40e052                                              0.0s
 => [internal] load build context                                                                                                                                        0.0s
 => => transferring context: 14.48kB                                                                                                                                     0.0s
 => CACHED [2/4] WORKDIR /src                                                                                                                                            0.0s
 => [3/4] ADD . .                                                                                                                                                        0.1s
 => [4/4] RUN CGO_ENABLED=0 go build -o go-lang-app .                                                                                                                   18.1s
 => exporting to image                                                                                                                                                   1.5s
 => => exporting layers                                                                                                                                                  1.5s
 => => writing image sha256:c24a911803f613f61baaa77adf93aec64da13d81e5ecb751243decda06c47e73                                                                             0.0s
 => => naming to docker.io/library/go-app:v2                                                                                                                             0.0s
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
go-app       v2        c24a911803f6   26 seconds ago   304MB
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker exec -it c24a911803f6 pwd
Error response from daemon: No such container: c24a911803f6
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker run -d -p 8090:8000 go-app:v2
9ce7f9d7c73106d1323ae00704e8f99cc70d176775623bda631f7401a795e426
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE       COMMAND           CREATED         STATUS         PORTS                                         NAMES
9ce7f9d7c731   go-app:v2   "./go-lang-app"   4 seconds ago   Up 4 seconds   0.0.0.0:8090->8000/tcp, [::]:8090->8000/tcp   pensive_albattani
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker exec -it 9ce7f9d7c731 pwd
/src
@mir-owahed ➜ /workspaces/go-lang-app (main) $ docker exec -it 9ce7f9d7c731 ls -la
total 6892
drwxr-xr-x    1 root     root          4096 Feb 20 09:31 .
drwxr-xr-x    1 root     root          4096 Feb 20 09:34 ..
drwxrwxrwx    9 root     root          4096 Feb 20 09:30 .git
-rw-rw-rw-    1 root     root            11 Feb 20 06:09 .gitignore
-rw-rw-rw-    1 root     root           126 Feb 20 06:09 Dockerfile
-rw-rw-rw-    1 root     root           399 Feb 20 06:09 README.md
-rw-rw-rw-    1 root     root          1283 Feb 20 07:04 command.txt
-rw-rw-rw-    1 root     root         11853 Feb 20 06:09 commands.txt
-rw-rw-rw-    1 root     root           246 Feb 20 06:09 dockerfile.multi
-rwxr-xr-x    1 root     root       7002878 Feb 20 09:31 go-lang-app
-rw-rw-rw-    1 root     root            52 Feb 20 06:09 go.mod
-rw-rw-rw-    1 root     root           623 Feb 20 06:09 hello.go

................................
@mir-owahed ➜ /workspaces/codespaces-blank $ ls
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps -a
CONTAINER ID   IMAGE                             COMMAND       CREATED        STATUS                        PORTS     NAMES
8601d5e3ead2   rockylinux:9.3.20231119-minimal   "/bin/bash"   2 hours ago    Exited (255) 34 seconds ago             rocky
2137842fe1da   rockylinux:9.3.20231119-minimal   "/bin/bash"   2 hours ago    Exited (0) 2 hours ago                  amazing_liskov
97fd4a300aee   centos                            "/bin/bash"   2 hours ago    Exited (255) 34 seconds ago             server
eed20b0e59bb   centos:latest                     "/bin/bash"   2 hours ago    Exited (0) 2 hours ago                  great_wozniak
9c4b120859de   hello-world:latest                "/hello"      15 hours ago   Exited (0) 15 hours ago                 musing_heisenberg
19063bd37478   hello-world:latest                "/hello"      15 hours ago   Exited (0) 15 hours ago                 optimistic_knuth
bd9bed75a951   hello-world                       "/sh"         15 hours ago   Created                                 boring_shtern
@mir-owahed ➜ /workspaces/codespaces-blank $ docker system prune -a
@mir-owahed ➜ /workspaces/codespaces-blank $ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
@mir-owahed ➜ /workspaces/codespaces-blank $ docker pull alpine
Using default tag: latest
latest: Pulling from library/alpine
f18232174bc9: Pull complete 
Digest: sha256:a8560b36e8b8210634f77d9f7f9efd7ffa463e380b75e2e74aff4511df3ef88c
Status: Downloaded newer image for alpine:latest
docker.io/library/alpine:latest
@mir-owahed ➜ /workspaces/codespaces-blank $ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
alpine       latest    aded1e1a5b37   11 days ago   7.83MB
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/codespaces-blank $ docker run -d -t --name server alpine
d108148f4e56afb3fec2be02352c0332fbe1b75923010fa436aceeb4a3ed3d00
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps
CONTAINER ID   IMAGE     COMMAND     CREATED         STATUS         PORTS     NAMES
d108148f4e56   alpine    "/bin/sh"   6 seconds ago   Up 5 seconds             server
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it d108148f4e56 ls -la
total 64
drwxr-xr-x    1 root     root          4096 Feb 25 08:53 .
drwxr-xr-x    1 root     root          4096 Feb 25 08:53 ..
-rwxr-xr-x    1 root     root             0 Feb 25 08:53 .dockerenv
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 bin
drwxr-xr-x    5 root     root           360 Feb 25 08:53 dev
drwxr-xr-x    1 root     root          4096 Feb 25 08:53 etc
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 home
drwxr-xr-x    6 root     root          4096 Feb 13 23:04 lib
drwxr-xr-x    5 root     root          4096 Feb 13 23:04 media
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 mnt
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 opt
dr-xr-xr-x  231 root     root             0 Feb 25 08:53 proc
drwx------    2 root     root          4096 Feb 13 23:04 root
drwxr-xr-x    3 root     root          4096 Feb 13 23:04 run
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 sbin
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 srv
dr-xr-xr-x   12 root     root             0 Feb 25 08:53 sys
drwxrwxrwt    2 root     root          4096 Feb 13 23:04 tmp
drwxr-xr-x    7 root     root          4096 Feb 13 23:04 usr
drwxr-xr-x   11 root     root          4096 Feb 13 23:04 var

@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it d108148f4e56 sh
/ # ls
bin    dev    etc    home   lib    media  mnt    opt    proc   root   run    sbin   srv    sys    tmp    usr    var
/ # mkdir test
/ # ls
bin    dev    etc    home   lib    media  mnt    opt    proc   root   run    sbin   srv    sys    test   tmp    usr    var
/ # pwd
/
/ # whoami
root
/ # yum update
sh: yum: not found
/ # dnf update
sh: dnf: not found
/ # ls -la
total 68
drwxr-xr-x    1 root     root          4096 Feb 25 08:56 .
drwxr-xr-x    1 root     root          4096 Feb 25 08:56 ..
-rwxr-xr-x    1 root     root             0 Feb 25 08:53 .dockerenv
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 bin
drwxr-xr-x    5 root     root           360 Feb 25 08:53 dev
drwxr-xr-x    1 root     root          4096 Feb 25 08:53 etc
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 home
drwxr-xr-x    6 root     root          4096 Feb 13 23:04 lib
drwxr-xr-x    5 root     root          4096 Feb 13 23:04 media
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 mnt
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 opt
dr-xr-xr-x  224 root     root             0 Feb 25 08:53 proc
drwx------    1 root     root          4096 Feb 25 08:55 root
drwxr-xr-x    3 root     root          4096 Feb 13 23:04 run
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 sbin
drwxr-xr-x    2 root     root          4096 Feb 13 23:04 srv
dr-xr-xr-x   12 root     root             0 Feb 25 08:53 sys
drwxr-xr-x    2 root     root          4096 Feb 25 08:56 test
drwxrwxrwt    2 root     root          4096 Feb 13 23:04 tmp
drwxr-xr-x    7 root     root          4096 Feb 13 23:04 usr
drwxr-xr-x   11 root     root          4096 Feb 13 23:04 var
/ # cat /etc/os-release 
NAME="Alpine Linux"
ID=alpine
VERSION_ID=3.21.3
PRETTY_NAME="Alpine Linux v3.21"
HOME_URL="https://alpinelinux.org/"
BUG_REPORT_URL="https://gitlab.alpinelinux.org/alpine/aports/-/issues"
/ # lsb_release -d
sh: lsb_release: not found
/ # exit

@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps -a
CONTAINER ID   IMAGE     COMMAND     CREATED         STATUS         PORTS     NAMES
d108148f4e56   alpine    "/bin/sh"   6 minutes ago   Up 6 minutes             server
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it d108148f4e56 /b
bin/  boot/ 
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it d108148f4e56 /b
bin/  boot/ 
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it d108148f4e56 /bin/bas
base32    base64    basename  bash      bashbug   
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it d108148f4e56 /bin/bash
OCI runtime exec failed: exec failed: unable to start container process: exec: "/bin/bash": stat /bin/bash: no such file or directory: unknown
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it d108148f4e56 /bin/sh
/ # exit
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps -a
CONTAINER ID   IMAGE     COMMAND     CREATED         STATUS         PORTS     NAMES
d108148f4e56   alpine    "/bin/sh"   9 minutes ago   Up 9 minutes             server
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps
CONTAINER ID   IMAGE     COMMAND     CREATED         STATUS         PORTS     NAMES
d108148f4e56   alpine    "/bin/sh"   9 minutes ago   Up 9 minutes             server
@mir-owahed ➜ /workspaces/codespaces-blank $ docker stop d108148f4e56
d108148f4e56
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps -a
CONTAINER ID   IMAGE     COMMAND     CREATED          STATUS                            PORTS     NAMES
d108148f4e56   alpine    "/bin/sh"   11 minutes ago   Exited (137) About a minute ago             server
@mir-owahed ➜ /workspaces/codespaces-blank $ docker rm d108148f4e56
d108148f4e56
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/codespaces-blank $ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
alpine       latest    aded1e1a5b37   11 days ago   7.83MB
@mir-owahed ➜ /workspaces/codespaces-blank $ docker rmi aded1e1a5b37
Untagged: alpine:latest
Untagged: alpine@sha256:a8560b36e8b8210634f77d9f7f9efd7ffa463e380b75e2e74aff4511df3ef88c
Deleted: sha256:aded1e1a5b3705116fa0a92ba074a5e0b0031647d9c315983ccba2ee5428ec8b
Deleted: sha256:08000c18d16dadf9553d747a58cf44023423a9ab010aab96cf263d2216b8b350
@mir-owahed ➜ /workspaces/codespaces-blank $
   30  history
@mir-owahed ➜ /workspaces/codespaces-blank $ docker system prune -a
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all images without at least one container associated to them
  - all build cache

Are you sure you want to continue? [y/N] y
Total reclaimed space: 0B



```


