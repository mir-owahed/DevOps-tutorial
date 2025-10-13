# Docker container hands-on — line-by-line explanation for beginners

Below I break the transcript into logical sections and explain each step plainly, point-wise, with the exact actions and why they matter. Treat this as a guided walk-through you can follow on your own machine.

---

## 1) Video intro — what to expect

## The speaker greets viewers and says this is a hands-on Docker container tutorial.

    
    → Expect practical commands and a demo environment.

---

## 2) What is a container? (concept)

## A container packages an application **and all its dependencies** so the app runs reliably across machines.

## Without containers, you must manually install the language/runtime and libraries on every machine where you run the code. The transcript explains that process and its pain points. ## With Docker, you build a portable image once; then the image runs as a container on any machine that has Docker installed. Only the Docker runtime is required as a prerequisite.

---

## 3) Prerequisite: Docker (and alternatives)

## The only required prerequisite to run containerized apps is a container runtime (Docker is used in the video). The transcript mentions other runtimes exist (e.g., *Fryo* — likely a spoken variant).

## The speaker uses Docker on an Ubuntu VM (so you need Docker installed inside whatever host you use).

---

## 4) Demo environment: VirtualBox + Ubuntu VM

## The presenter runs Docker inside an **Ubuntu virtual machine** created with Oracle VirtualBox on Windows. He shows how he starts that VM before running Docker commands.

## If you follow along on Windows, you can either install Docker Desktop or create an Ubuntu VM and install Docker there. The transcript uses an Ubuntu VM approach.

---

## 5) Installing Docker on Ubuntu — high level steps

## Open a terminal (Ctrl+T in Ubuntu). Check whether Docker is installed by running a version check: `docker --version` (transcript shows the speaker checking and seeing it is not installed).

## Follow the official install instructions (the speaker opens a browser, searches “install Docker on Ubuntu”, and uses the apt repository commands). The typical sequence he demonstrates is: add Docker’s apt repository, install packages, then install Docker Engine. ## Commands in transcript: copy repository setup command, run it, enter sudo password, wait for packages to install. (Transcript repeatedly emphasizes waiting for network/Internet speeds.)

---

## 6) Post-install steps (permissions)

## After installation, `docker --version` may show “permission denied” because Docker needs root or a user in the `docker` group.

## The transcript shows the post-installation steps:
    - Add your user to the docker group: `sudo usermod -aG docker <your-username>` (transcript describes `sudo group adduser` style — correct modern command is `sudo usermod -aG docker $**USER**`).
    - Log out and log back in (or restart your terminal/VM) so group membership is re-evaluated.
## Then re-run `docker --version` or a test run to confirm you can access Docker without `sudo`.

---

## 7) Quick test: `docker run hello-world`

## After install and permission fix, run: `docker run hello-world`. This downloads the official `hello-world` image and executes it, confirming Docker works. The transcript shows this as the canonical confirmation.

---

## 8) Why containers vs virtual machines (comparison)

## Virtual machines use a hypervisor and each VM runs a full guest OS — heavy weight. Containers share the host kernel and are much lighter.

## The transcript explains: VM = full OS per VM; container = lightweight, uses kernel features to isolate workloads. This is why containers are faster and more resource-efficient.

---

## 9) Docker lifecycle (build → image → run)

## High-level flow in the video:

    - Write code (app).
    - Create a `Dockerfile` (text instructions describing how to build the image).
    - Run `docker build` to create a Docker image from the `Dockerfile`.
    - Run `docker run` to start a container from that image.

---

## 10) Example demo app (Go / Golang)

## The demo app is a small Golang API (has endpoints like `/ping` and `/hello`). The code is hosted in a GitHub repo that the presenter clones.

## Steps to get the code: ensure `git` is installed, copy the repo URL and run `git clone <repo-url>`. Then `ls` to inspect repository files; the repo already contains a `Dockerfile`.

---

## 11) The Dockerfile — what each part means (transcript example)

The transcript shows a `Dockerfile` for an Alpine-based Go image. Key directives explained:

1. `**FROM** golang:1.22-alpine` — base image that provides Go compiler/runtime on a lightweight Alpine Linux. (Base image gives you the build environment.)
2. `**WORKDIR** /research` — sets the working directory inside the image; subsequent commands run relative to this path.
3. `**ADD** . .` (or `**COPY** . .`) — adds your application source code into the image at the working directory.
4. `**RUN** go build -o GolangApp .` — runs the build inside the image, producing a binary named `GolangApp`. `o` sets output filename; `.` indicates current directory.
5. `**EXPOSE** **8000**` — documents (and hints to Docker) that the app listens on container port `**8000**`. This does not automatically publish the port — `docker run -p host:container` is needed.
6. `**CMD** [*./GolangApp*]` or similar — runs the built binary when the container starts. The transcript shows running the binary `./GolangApp`.

---

## 12) Build the image

## Use `docker build -t go-app:V1 .` (the `t` flag assigns a tag/name). The dot (`.`) indicates the Dockerfile and build context are in the current directory.

## Docker builds images layer by layer. The transcript shows progress like `1/4`, `2/4` — each directive becomes a layer. ## After build completes, use `docker images` to confirm the image exists.

---

## 13) Run the container and port mapping

## Run the container detached (in background) and map container port `8000` to host port `8080` (example):

    
    ```bash
    docker run -d -p **8080**:**8000** go-app:V1
    
    ```
    
    - `d` = detached, `p host:container` = publish port mapping.
## Access APIs in browser: `[http://localhost:8080/ping`](http://localhost:8080/ping`) should return `pong`; `[http://localhost:8080/hello`](http://localhost:8080/hello`) should return `hello world` (depending on repo's endpoints). The transcript demonstrates this behavior.

---

## 14) Inspect running containers

1. `docker ps` — shows running containers (IDs, names, ports). `docker ps -a` shows all containers including stopped ones. The transcript repeatedly uses both.
## To stop a container: `docker stop <container-id>` (or container name). The transcript shows copying the container ID and stopping it.
## Start a stopped container: `docker start <container-id>`. The transcript demonstrates restarting then accessing the app again.

---

## 15) Remove containers and images

## Remove a stopped container: `docker rm <container-id>`. The transcript demonstrates stopping then removing.

## Remove an image: `docker rmi <image-id>` — you **must** remove containers that use the image first (otherwise `docker rmi` will fail). The transcript shows this exact behavior.

---

## 16) Entering (exec) into a container

## Use `docker exec -it <container-id> /bin/bash` or `/bin/sh` to open an interactive shell in the running container. In Alpine images you usually use `/bin/sh`. The transcript demonstrates running `docker exec -it <id> /bin/sh`.

## Once inside, you can `ls -la`, view files (source, binary), create files (e.g., `touch`, `nano`), then exit to leave the container shell.

---

## 17) Docker Hub — pushing and pulling images

1. **Docker Hub** is a container registry to store images. The transcript shows logging into Docker Hub, creating a repo, and pushing an image.
## Typical push workflow from transcript:
    - Tag your local image for your Docker Hub namespace:
    
    ```bash
    docker tag go-app:V2 <dockerhub-username>/<repo-name>:V2
    
    ```
    
    - Login to Docker Hub (instructions in transcript mention using a personal access token):
    
    ```bash
    docker login --username <username>
    # paste token/password when prompted
    
    ```
    
    - Push: `docker push <dockerhub-username>/<repo-name>:V2` — this uploads the image layers to the registry. The transcript shows this and mentions it can take time (image sizes like **300**+ MB).
## Pulling an image: `docker pull <image-name>:<tag>` — transcript demonstrates pulling big images and re-running them locally.

---

## 18) Tagging and naming conventions

## Image name format for Docker Hub: `<namespace>/<repository>:<tag>` (e.g., `mir-owahed/go-app:V2`). The transcript emphasizes updating the tag with `docker tag` before pushing.

---

## 19) Useful commands (summary list from transcript)

(Commands shown exactly as used or described in the transcript)

- `docker --version` — check Docker installed.
- `docker run hello-world` — test Docker.
- `git clone <repo>` — clone example app.
- `docker build -t go-app:V1 .` — build image from Dockerfile.
- `docker images` — list images.
- `docker run -d -p **8080**:**8000** go-app:V1` — run container detached and map ports.
- `docker ps` / `docker ps -a` — show running/all containers.
- `docker stop <id>` — stop container.
- `docker rm <id>` — remove container.
- `docker rmi <image-id>` — remove image (after removing containers).
- `docker exec -it <id> /bin/sh` — open shell inside container (Alpine uses `sh`).
- `docker tag <old> <new>` — retag images for pushing.
- `docker login` + `docker push <name>` — login and push to Docker Hub.
- `docker pull <name>` — pull from Docker Hub.
- `docker inspect <container-id>` — show detailed metadata of container.
- `docker logs <container-id>` — view container logs.
- `docker system prune -a` — dangerous: removes stopped containers, unused networks, dangling images and build cache (transcript warns to use cautiously).

---

## 20) Logs and inspect

## Use `docker logs <id>` to see application output; when the Go app receives requests (e.g., `/ping`) the logs will show it — useful for debugging. Transcript demonstrates invoking `/ping` and seeing logs change.

2. `docker inspect <id>` prints **JSON** metadata: host ports, image **SHA**, volumes etc. Transcript shows using `docker inspect` to view host port and other details.

---

## 21) Final recap from transcript (what learner should take away)

## How to clone a repo with `git clone`.

## How to write/read a `Dockerfile` and what each directive does. ## How to build an image: `docker build`. ## How to list images: `docker images`. ## How to run an image as a container: `docker run -d -p host:container image:tag`. ## How to check containers: `docker ps` / `docker ps -a`. ## How to stop/remove containers and remove images. ## How to push/pull images to/from Docker Hub after tagging and logging in. ## How to get inside containers (`docker exec`) and inspect logs/metadata.

---

## 22) Common pitfalls & tips (derived from transcript)

1. **Permission denied** — fix by adding user to `docker` group and re-logging in.
2. **Port confusion** — map container port to host port correctly (`p host:container`), and remember `**EXPOSE**` only documents the port.
3. **Cannot remove image** — must stop and remove containers using that image first. Transcript shows `docker rmi` failing until container removed.
4. **Large images take time** — pushing/pulling big images (100s of MBs) is slow; be patient and check network speed.
5. **Alpine shells** — some images use `/bin/sh` (not `/bin/bash`) — use the appropriate shell when `exec`ing.

---

## 23) Short cheat-sheet (copy/paste)

```bash # check docker docker --version

# test

docker run hello-world

# build (from folder with Dockerfile)

docker build -t myapp:V1 .

# list images

docker images

# run container (detached, port map)

docker run -d -p **8080**:**8000** myapp:V1

# list running containers

docker ps

# list all containers (including stopped)

docker ps -a

# stop and remove container

docker stop <container-id> docker rm <container-id>

# remove image

docker rmi <image-id>

# exec into container (Alpine -> /bin/sh)

docker exec -it <container-id> /bin/sh

# logs & inspect

docker logs <container-id> docker inspect <container-id>

# tag, login and push

docker tag myapp:V1 <username>/myapp:V1 docker login docker push <username>/myapp:V1

# pull

docker pull <username>/myapp:V1

# clean up (use with caution)

docker system prune -a

```

(These commands follow the transcript examples.)
