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
wget https://go.dev/dl/go1.22.5.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz
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
### Dockerfile
```
FROM golang:1.22-alpine

WORKDIR /src
ADD . .
RUN CGO_ENABLED=0 go build -o go-lang-app .
EXPOSE 8000
CMD ["./go-lang-app"]
```
