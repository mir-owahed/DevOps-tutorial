```
248  docker --version
  249  docker images
  250  docker images fda1f6976755
  251  docker images 
  252  docker rmi fda1f6976755
  253  docker rmi 98ca9b5cd278
  254  docker ps
  255  docker ps -a
  256  docker stop 78dfbbb366b9
  257  docker stop 4dcc61c6b62e
  258  docker images
  259  docker rmi 98ca9b5cd278
  260  docker images
  261  docker ps -a
  262  docker rm 78dfbbb366b9
  263  docker rm 4dcc61c6b62e
  264  docker images
  265  docker rmi 98ca9b5cd278
  266  ls
  267  docker build -t python-hello-app .
  268  docker images
  269  docker tag --help
  270  docker tag python-hello-app:latest owahed1/python-sample-app:0.0.1
  271  docker images
  272  docker rmi 7c92261ad4fa
  273  docker rmi -f 7c92261ad4fa
  274  docker login
  275  docker push owahed1/python-sample-app:0.0.1
  276  docker images
  277  docker build -t python-hello-app .
  278  docker tag python-hello-app:latest owahed1/python-sample-app:0.0.1
  279  docker images
  280  docker push owahed1/python-sample-app:0.0.1
  281  docker images
  282  docker rmi owahed1/python-sample-app:0.0.1
  283  docker images
  284  docker rmi python-hello-app:latest
  285  docker images
  286  clear
  287  docker pull owahed1/python-sample-app:0.0.1
  288  docker images
  289  ls
  290  cat app.py 
  291  ddocker run -p 8000:5000 owahed1/python-sample-app:0.0.1
  292  docker run -p 8000:5000 owahed1/python-sample-app:0.0.1
  293  exit
  294  history
  295  docker ps
  296  docker ps -a
  297  docker run -p -d 8000:5000 owahed1/python-sample-app:0.0.1
  298  docker run -d -p 8000:5000 owahed1/python-sample-app:0.0.1
  299  docker ps
  300  docker rm f4e58d9e0915
  301  docker stop f4e58d9e0915
  302  docker rm f4e58d9e0915
  303  docker ps
  304  docker ps -a
  305  docker run --rm -d -p 8001:5000 owahed1/python-sample-app:0.0.1
  306  curl http://localhost:8001/
  307  curl http://localhost:8001/ping
  308  docker ps
  309  docker stop 4f63990a881f
  310  docker ps
  311  docker run --rm -d -p 8001:5000 owahed1/python-sample-app:0.0.1
  312  docker ps
  313  docker exec -it a27c86738456 bash
  314  docker exec -it a27c86738456 ls -la
  315  docker exec -it a27c86738456 pwd
  316  docker exec -it a27c86738456 /bin/bash
  317  docker logs a27c86738456
  318  docker logs -f a27c86738456
  319  history
```
