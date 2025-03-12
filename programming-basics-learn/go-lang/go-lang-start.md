# How to run go lang app
Prerequisite:
Install go on your machine

Reference: 
1. <https://go.dev/doc/code>

2. <https://go.dev/doc/install>
```
Download go
tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version
go run .
go mod init github.com/mir-owahed/go-lang-app
go build
go test
```
Install go using cli on ubuntu
```
wget https://go.dev/dl/go1.24.1.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.24.1.linux-amd64.tar.gz
sudo nano .bashrc
add the below line
export PATH=$PATH:/usr/local/go/bin
go version
```
```
go run hello.go
go build hello.go
./hello (to run the executable)
go build -o application hello.go
```
# How to Build and Run go lang app
Clone the following Repo:
Reference: 
1. <https://github.com/mir-owahed/go-lang-app.git>
2. <https://github.com/mir-owahed/ultimate-devops-project-demo.git>
3. <https://github.com/mir-owahed/go-web-app.git>
4. <https://github.com/open-telemetry/opentelemetry-demo.git>




### Dockerfile
```
FROM golang:1.22-alpine

WORKDIR /src
ADD . .
RUN CGO_ENABLED=0 go build -o go-lang-app .
EXPOSE 8000
CMD ["./go-lang-app"]
```
