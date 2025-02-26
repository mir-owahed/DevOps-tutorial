docker-container-hands-on totorial
```
@mir-owahed ➜ /workspaces/codespaces-blank $ ls -la
total 8
drwxrwxrwx+ 2 codespace root 4096 Feb 25 16:40 .
drwxr-xrwx+ 5 codespace root 4096 Feb 25 16:40 ..
@mir-owahed ➜ /workspaces/codespaces-blank $ pwd
/workspaces/codespaces-blank
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
@mir-owahed ➜ /workspaces/codespaces-blank $ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
@mir-owahed ➜ /workspaces/codespaces-blank $ docker pull rockylinux
Using default tag: latest
Error response from daemon: manifest for rockylinux:latest not found: manifest unknown: manifest unknown
@mir-owahed ➜ /workspaces/codespaces-blank $ docker pull rockylinux:9.3.20231119-minimal
9.3.20231119-minimal: Pulling from library/rockylinux
8ec988941d66: Pull complete 
Digest: sha256:305de618a5681ff75b1d608fd22b10f362867dff2f550a4f1d427d21cd7f42b4
Status: Downloaded newer image for rockylinux:9.3.20231119-minimal
docker.io/library/rockylinux:9.3.20231119-minimal
@mir-owahed ➜ /workspaces/codespaces-blank $ docker images
REPOSITORY   TAG                    IMAGE ID       CREATED         SIZE
rockylinux   9.3.20231119-minimal   dfaa211c6b30   15 months ago   118MB
@mir-owahed ➜ /workspaces/codespaces-blank $ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
5a7813e071bf: Pull complete 
Digest: sha256:72297848456d5d37d1262630108ab308d3e9ec7ed1c3286a32fe09856619a782
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
@mir-owahed ➜ /workspaces/codespaces-blank $ docker images
REPOSITORY   TAG                    IMAGE ID       CREATED         SIZE
ubuntu       latest                 a04dc4851cbc   4 weeks ago     78.1MB
rockylinux   9.3.20231119-minimal   dfaa211c6b30   15 months ago   118MB
@mir-owahed ➜ /workspaces/codespaces-blank $ docker run -d -t --name ubuntu-container ubuntu
569afeff52132672ca40736daf1476c7dc5c7eac0435081151e4528eae3b6196
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS         PORTS     NAMES
569afeff5213   ubuntu    "/bin/bash"   6 seconds ago   Up 5 seconds             ubuntu-container
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it 569afeff5213 /bin/bash
root@569afeff5213:/# ls -la
total 56
drwxr-xr-x   1 root root 4096 Feb 26 09:57 .
drwxr-xr-x   1 root root 4096 Feb 26 09:57 ..
-rwxr-xr-x   1 root root    0 Feb 26 09:57 .dockerenv
lrwxrwxrwx   1 root root    7 Apr 22  2024 bin -> usr/bin
drwxr-xr-x   2 root root 4096 Apr 22  2024 boot
drwxr-xr-x   5 root root  360 Feb 26 09:57 dev
drwxr-xr-x   1 root root 4096 Feb 26 09:57 etc
drwxr-xr-x   3 root root 4096 Jan 27 02:09 home
lrwxrwxrwx   1 root root    7 Apr 22  2024 lib -> usr/lib
lrwxrwxrwx   1 root root    9 Apr 22  2024 lib64 -> usr/lib64
drwxr-xr-x   2 root root 4096 Jan 27 02:03 media
drwxr-xr-x   2 root root 4096 Jan 27 02:03 mnt
drwxr-xr-x   2 root root 4096 Jan 27 02:03 opt
dr-xr-xr-x 223 root root    0 Feb 26 09:57 proc
drwx------   2 root root 4096 Jan 27 02:09 root
drwxr-xr-x   4 root root 4096 Jan 27 02:09 run
lrwxrwxrwx   1 root root    8 Apr 22  2024 sbin -> usr/sbin
drwxr-xr-x   2 root root 4096 Jan 27 02:03 srv
dr-xr-xr-x  12 root root    0 Feb 26 09:57 sys
drwxrwxrwt   2 root root 4096 Jan 27 02:09 tmp
drwxr-xr-x  12 root root 4096 Jan 27 02:03 usr
drwxr-xr-x  11 root root 4096 Jan 27 02:09 var
root@569afeff5213:/# apt update
Get:1 http://archive.ubuntu.com/ubuntu noble InRelease [256 kB]
Get:2 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Get:3 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Packages [1053 kB]
Get:4 http://archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
Get:5 http://archive.ubuntu.com/ubuntu noble-backports InRelease [126 kB]
Get:6 http://archive.ubuntu.com/ubuntu noble/multiverse amd64 Packages [331 kB]     
Get:7 http://archive.ubuntu.com/ubuntu noble/restricted amd64 Packages [117 kB]             
Get:8 http://archive.ubuntu.com/ubuntu noble/universe amd64 Packages [19.3 MB]              
Get:9 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Packages [822 kB]                  
Get:10 http://archive.ubuntu.com/ubuntu noble/main amd64 Packages [1808 kB]          
Get:11 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Packages [28.8 kB]
Get:12 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 Packages [1119 kB]
Get:13 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Packages [863 kB]
Get:14 http://security.ubuntu.com/ubuntu noble-security/main amd64 Packages [798 kB]
Get:15 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 Packages [1331 kB]  
Get:16 http://archive.ubuntu.com/ubuntu noble-backports/universe amd64 Packages [16.0 kB]
Get:17 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Packages [24.2 kB]
Fetched 28.3 MB in 5s (6070 kB/s)                          
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
18 packages can be upgraded. Run 'apt list --upgradable' to see them.
root@569afeff5213:/# cd /home/ubuntu/
root@569afeff5213:/home/ubuntu# ls
root@569afeff5213:/home/ubuntu# lab_release -d
bash: lab_release: command not found
root@569afeff5213:/home/ubuntu# exit
exit
@mir-owahed ➜ /workspaces/codespaces-blank $ docker images
REPOSITORY   TAG                    IMAGE ID       CREATED         SIZE
ubuntu       latest                 a04dc4851cbc   4 weeks ago     78.1MB
rockylinux   9.3.20231119-minimal   dfaa211c6b30   15 months ago   118MB
@mir-owahed ➜ /workspaces/codespaces-blank $ docker run -d -t --name rocky-server rockylinux
Unable to find image 'rockylinux:latest' locally
docker: Error response from daemon: manifest for rockylinux:latest not found: manifest unknown: manifest unknown.
See 'docker run --help'.
@mir-owahed ➜ /workspaces/codespaces-blank $ docker run -d -t --name rocky-server rockylinux:9.3.20231119-minimal
c504e4e4b678117fe4adefea16839672454c596dd876be4aa03af83a0517b4a0
@mir-owahed ➜ /workspaces/codespaces-blank $ docker ps
CONTAINER ID   IMAGE                             COMMAND       CREATED          STATUS          PORTS     NAMES
c504e4e4b678   rockylinux:9.3.20231119-minimal   "/bin/bash"   4 seconds ago    Up 4 seconds              rocky-server
569afeff5213   ubuntu                            "/bin/bash"   11 minutes ago   Up 11 minutes             ubuntu-container
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it c504e4e4b678 /bin/sh
sh-5.1# yum update
sh: yum: command not found
sh-5.1# ls -la
total 60
drwxr-xr-x   1 root root 4096 Feb 26 10:09 .
drwxr-xr-x   1 root root 4096 Feb 26 10:09 ..
-rwxr-xr-x   1 root root    0 Feb 26 10:09 .dockerenv
dr-xr-xr-x   2 root root 4096 May 16  2022 afs
lrwxrwxrwx   1 root root    7 May 16  2022 bin -> usr/bin
drwxr-xr-x   5 root root  360 Feb 26 10:09 dev
drwxr-xr-x   1 root root 4096 Feb 26 10:09 etc
drwxr-xr-x   2 root root 4096 May 16  2022 home
lrwxrwxrwx   1 root root    7 May 16  2022 lib -> usr/lib
lrwxrwxrwx   1 root root    9 May 16  2022 lib64 -> usr/lib64
drwx------   2 root root 4096 Nov 19  2023 lost+found
drwxr-xr-x   2 root root 4096 May 16  2022 media
drwxr-xr-x   2 root root 4096 May 16  2022 mnt
drwxr-xr-x   2 root root 4096 May 16  2022 opt
dr-xr-xr-x 225 root root    0 Feb 26 10:09 proc
dr-xr-x---   2 root root 4096 Nov 19  2023 root
drwxr-xr-x   2 root root 4096 Nov 19  2023 run
lrwxrwxrwx   1 root root    8 May 16  2022 sbin -> usr/sbin
drwxr-xr-x   2 root root 4096 May 16  2022 srv
dr-xr-xr-x  12 root root    0 Feb 26 10:04 sys
drwxrwxrwt   2 root root 4096 Nov 19  2023 tmp
drwxr-xr-x  12 root root 4096 Nov 19  2023 usr
drwxr-xr-x  18 root root 4096 Nov 19  2023 var
sh-5.1# exit
exit
@mir-owahed ➜ /workspaces/codespaces-blank $ docker exec -it c504e4e4b678 ls -la
total 60
drwxr-xr-x   1 root root 4096 Feb 26 10:09 .
drwxr-xr-x   1 root root 4096 Feb 26 10:09 ..
-rwxr-xr-x   1 root root    0 Feb 26 10:09 .dockerenv
dr-xr-xr-x   2 root root 4096 May 16  2022 afs
lrwxrwxrwx   1 root root    7 May 16  2022 bin -> usr/bin
drwxr-xr-x   5 root root  360 Feb 26 10:09 dev
drwxr-xr-x   1 root root 4096 Feb 26 10:09 etc
drwxr-xr-x   2 root root 4096 May 16  2022 home
lrwxrwxrwx   1 root root    7 May 16  2022 lib -> usr/lib
lrwxrwxrwx   1 root root    9 May 16  2022 lib64 -> usr/lib64
drwx------   2 root root 4096 Nov 19  2023 lost+found
drwxr-xr-x   2 root root 4096 May 16  2022 media
drwxr-xr-x   2 root root 4096 May 16  2022 mnt
drwxr-xr-x   2 root root 4096 May 16  2022 opt
dr-xr-xr-x 225 root root    0 Feb 26 10:09 proc
dr-xr-x---   1 root root 4096 Feb 26 10:11 root
drwxr-xr-x   2 root root 4096 Nov 19  2023 run
lrwxrwxrwx   1 root root    8 May 16  2022 sbin -> usr/sbin
drwxr-xr-x   2 root root 4096 May 16  2022 srv
dr-xr-xr-x  12 root root    0 Feb 26 10:04 sys
drwxrwxrwt   2 root root 4096 Nov 19  2023 tmp
drwxr-xr-x  12 root root 4096 Nov 19  2023 usr
drwxr-xr-x  18 root root 4096 Nov 19  2023 var
@mir-owahed ➜ /workspaces/codespaces-blank $ git clone https://github.com/mir-owahed/go-lang-app.git
Cloning into 'go-lang-app'...
remote: Enumerating objects: 36, done.
remote: Counting objects: 100% (36/36), done.
remote: Compressing objects: 100% (32/32), done.
remote: Total 36 (delta 15), reused 17 (delta 3), pack-reused 0 (from 0)
Receiving objects: 100% (36/36), 8.84 KiB | 8.84 MiB/s, done.
Resolving deltas: 100% (15/15), done.
@mir-owahed ➜ /workspaces/codespaces-blank $ ls
go-lang-app
@mir-owahed ➜ /workspaces/codespaces-blank $ cd go-lang-app/
@mir-owahed ➜ /workspaces/codespaces-blank/go-lang-app (main) $ ls
Dockerfile  README.md  command.txt  commands.txt  dockerfile.multi  go.mod  hello.go
@mir-owahed ➜ /workspaces/codespaces-blank/go-lang-app (main) $ docker build -t go-app:v1 .
[+] Building 31.1s (10/10) FINISHED                                                                                                                                                                      docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                               0.0s
 => => transferring dockerfile: 163B                                                                                                                                                                               0.0s
 => [internal] load metadata for docker.io/library/golang:1.22-alpine                                                                                                                                              2.2s
 => [auth] library/golang:pull token for registry-1.docker.io                                                                                                                                                      0.0s
 => [internal] load .dockerignore                                                                                                                                                                                  0.0s
 => => transferring context: 2B                                                                                                                                                                                    0.0s
 => [1/4] FROM docker.io/library/golang:1.22-alpine@sha256:1699c10032ca2582ec89a24a1312d986a3f094aed3d5c1147b19880afe40e052                                                                                       10.0s
 => => resolve docker.io/library/golang:1.22-alpine@sha256:1699c10032ca2582ec89a24a1312d986a3f094aed3d5c1147b19880afe40e052                                                                                        0.0s
 => => sha256:afa154b433c7f72db064d19e1bcfa84ee196ad29120328f6bdb2c5fbd7b8eeac 69.36MB / 69.36MB                                                                                                                   1.7s
 => => sha256:1699c10032ca2582ec89a24a1312d986a3f094aed3d5c1147b19880afe40e052 10.30kB / 10.30kB                                                                                                                   0.0s
 => => sha256:6d405dfc5fdf3a45df1529cf060b920041f52ce523487e0f36f02765af294a51 1.92kB / 1.92kB                                                                                                                     0.0s
 => => sha256:4129f51f28c9ae5de799b958ba2aaa8f92f26cc7bf47c107891673fe4b516c03 2.08kB / 2.08kB                                                                                                                     0.0s
 => => sha256:1f3e46996e2966e4faa5846e56e76e3748b7315e2ded61476c24403d592134f0 3.64MB / 3.64MB                                                                                                                     0.3s
 => => sha256:4d75fd4b73869ed224045c010cdec78756eefb6752a5a8e4804294009eac11e9 294.90kB / 294.90kB                                                                                                                 0.7s
 => => extracting sha256:1f3e46996e2966e4faa5846e56e76e3748b7315e2ded61476c24403d592134f0                                                                                                                          0.1s
 => => sha256:5f837c998576dcb54bc285997f33fcc2166dff6aa48fe3a374da92474efd5fe8 126B / 126B                                                                                                                         0.6s
 => => extracting sha256:4d75fd4b73869ed224045c010cdec78756eefb6752a5a8e4804294009eac11e9                                                                                                                          0.1s
 => => sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1 32B / 32B                                                                                                                           1.7s
 => => extracting sha256:afa154b433c7f72db064d19e1bcfa84ee196ad29120328f6bdb2c5fbd7b8eeac                                                                                                                          4.6s
 => => extracting sha256:5f837c998576dcb54bc285997f33fcc2166dff6aa48fe3a374da92474efd5fe8                                                                                                                          0.0s
 => => extracting sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1                                                                                                                          0.0s
 => [internal] load build context                                                                                                                                                                                  0.0s
 => => transferring context: 58.49kB                                                                                                                                                                               0.0s
 => [2/4] WORKDIR /src                                                                                                                                                                                             0.0s
 => [3/4] ADD . .                                                                                                                                                                                                  0.0s
 => [4/4] RUN CGO_ENABLED=0 go build -o go-lang-app .                                                                                                                                                             17.2s
 => exporting to image                                                                                                                                                                                             1.6s
 => => exporting layers                                                                                                                                                                                            1.6s
 => => writing image sha256:2f6db502a926b99a1ce30f5f2406e81e759b3646c90a5bc7bb7a2c8b987a7352                                                                                                                       0.0s
 => => naming to docker.io/library/go-app:v1                                                                                                                                                                       0.0s
@mir-owahed ➜ /workspaces/codespaces-blank/go-lang-app (main) $ docker images
REPOSITORY   TAG                    IMAGE ID       CREATED          SIZE
go-app       v1                     2f6db502a926   59 seconds ago   304MB
ubuntu       latest                 a04dc4851cbc   4 weeks ago      78.1MB
rockylinux   9.3.20231119-minimal   dfaa211c6b30   15 months ago    118MB
@mir-owahed ➜ /workspaces/codespaces-blank/go-lang-app (main) $ docker run -d -p 8080:8000 go-app:v1
4cc565a675dcb87d76003ac4b606c397c0f209221594ca9726686035a62e8706
@mir-owahed ➜ /workspaces/codespaces-blank/go-lang-app (main) $ docker ps
CONTAINER ID   IMAGE                             COMMAND           CREATED          STATUS          PORTS                                         NAMES
4cc565a675dc   go-app:v1                         "./go-lang-app"   5 seconds ago    Up 4 seconds    0.0.0.0:8080->8000/tcp, [::]:8080->8000/tcp   blissful_jones
c504e4e4b678   rockylinux:9.3.20231119-minimal   "/bin/bash"       17 minutes ago   Up 17 minutes                                                 rocky-server
569afeff5213   ubuntu                            "/bin/bash"       29 minutes ago   Up 29 minutes                                                 ubuntu-container
@mir-owahed ➜ /workspaces/codespaces-blank/go-lang-app (main) $ 
```
