# Linux Ubuntu commands
```
    1  sudo su

    2  su -

    3  su - root

    4  cd

    5  history

    6  su root

    7  su -

    8  sudo su

    9  sudo visudo

   10  su -

   11  sudo apt update

   12  sudo apt-get install wget gpg

   13  wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg

   14  sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg

   15  sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'

   16  rm -f packages.microsoft.gpg

   17  sudo apt install apt-transport-https

   18  sudo apt update

   19  sudo apt install code

   20  ls

   21  cd Documents/

   22  ls

   23  mkdir python-app

   24  cd python-app/

   25  code .

   26  curl http://localhost:81

   27  sudo apt install curl

   28  curl http://localhost:81

   29  curl http://localhost:81/ping

   30  curl http://localhost:81/hello

   31  curl http://localhost:81/ping

   32  curl http://localhost:81/hello

   33  curl http://localhost:81/ping

   34  curl http://localhost:81/

   35  history

   36  cd Documents/python-app/

   37  history

   38  history >> commands.txt 

   39  python3 -V

   40  pip3 -V

   41  sudo apt install python3 python3-pip build-essential python3-dev

   42  python3 -V

   43  pip3 -V

   44  sudo pip3 install -r requirements.txt

   45  python3 app.py 

   46  sudo pip3 install -r requirements.txt

   47  python3 app.py 

   48  sudo pip3 install flask

   49  python3 app.py 

   50  sudo python3 app.py 

   51  history > commands.txt

   52  ls

   53  history

   54  git -V

   55  git --version

   56  git remote -V

   57  git init

   58  git status

   59  git add .

   60  git status

   61  git commit -m "python flask app"

   62  git log

   63  git remote -V

   64  git remote -v

   65  git log

   66  git branch -M main

   67  git log

   68  git remote add origin https://github.com/mir-owahed/python-flask-app.git

   69  git remote -v

   70  git push -u origin main

   71  history

   72  git status

   73  git commit -am "commands updated"

   74  git status

   75  git push -u origin main

   76  node -v

   77  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

   78  nvm install node

   79  command -v nvm

   80  nvm install node

   81  npm -v

   82  node app.js 

   83  history

   84  node app.js 

   85  code .

   86  history

   87  ls

   88  history

   89  exit

   90  curl http://localhost:8080

   91  java --version

   92  sudo apt install openjdk-11-jdk-headless

   93  java --version

   94  mvn --version

   95  sudo apt install maven

   96  mvn --version

   97  mvn compile

   98  javac --version

   99  java 17

  100  sudo apt install openjdk-17-jdk

  101  mvn compile

  102  ls

  103  mvn package

  104  ls

  105  cd target/

  106  ls

  107  java -jar javaSpringProj-0.0.1-SNAPSHOT.jar 

  108  curl http://localhost:8080/

  109  curl http://localhost:8080

  110  java -jar javaSpringProj-0.0.1-SNAPSHOT.jar 

  111  mvn test

  112  mvn clean package

  113  cd ..

  114  mvn test

  115  cd target/

  116  ls

  117  java -jar javaSpringProj-0.0.1-SNAPSHOT.jar 

  118  cd ..

  119  mvn clean package

  120  ls

  121  mvn test

  122  mvn clean package

  123  java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 

  124  history

  125  ls

  126  mv javaSpringProj.zip  ~/Documents/

  127  ls

  128  cd 

  129  cd Documents/

  130  ls

  131  unzip javaSpringProj.zip 

  132  ls

  133  cd javaSpringProj/

  134  ls

  135  code .

  136  history

  137  curl 127.0.0.1:9000

  138  ls

  139  cd target/

  140  ll

  141  ls

  142  mvn test

  143  cd ..

  144  mvn compile

  145  mvn test

  146  mvn clean package

  147  java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 

  148  mvn clean package

  149  java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 

  150  ls

  151  cd target/

  152  ls

  153  cd ..

  154  mvn clean package

  155  java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 

  156  mvn test

  157  mvn clean

  158  mvn test

  159  mvn clean

  160  mvn clean package

  161  java -jar target/javaSpringProj-0.0.1-SNAPSHOT.jar 

  162  history

  163  code .

  164  npm run dev

  165  npm run build

  166  npm run dev

  167  npm run build

  168  npm run dev

  169  npm run build

  170  npm run dev

  171  npm run build

  172  git init

  173  git status

  174  git add .

  175  git commit "react frontend hello world app"

  176  git commit -m "react frontend hello world app"

  177  git status

  178  git remote -v

  179  git remote -V

  180  git remote -v

  181  git remote add origin https://github.com/mir-owahed/react-app.git

  182  git remote -v

  183  git npx create-next-app@latest

  184  cd react-app/

  185  code .

  186  npm run dev

  187  npm run build

  188  npm start

  189  code .

  190  docker ps

  191  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

  192  sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

  193  # Add Docker's official GPG key:

  194  sudo apt-get update

  195  sudo apt-get install ca-certificates curl

  196  sudo install -m 0755 -d /etc/apt/keyrings

  197  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

  198  sudo chmod a+r /etc/apt/keyrings/docker.asc

  199  # Add the repository to Apt sources:

  200  echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \

  201    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

  202  sudo apt-get update

  203  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

  204  sudo groupadd docker

  205  sudo usermod -aG $USER

  206  sudo usermod -aG docker $USER

  207  docker help

  208  clear

  209  docker --version

  210  docker ps 

  211  sudo usermod -aG docker $USER

  212  docker ps -a

  213  minikube start --nodes 2

  214  kubectl --help

  215  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

  216  kubectl --help

  217  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

  218  ls

  219  kubectl --help

  220  ls -la

  221  clear

  222  ls -la

  223  vim .config/

  224  sudo apt install vim

  225  vim .config/

  226  ls -a

  227  vim .bashrc 

  228  k get nodes

  229  docker ps

  230  sudo groupadd docker

  231  newgrp docker

  232  kubectl get nodes

  233  k get nodes

  234  vim .bashrc 

  235  k get nodes

  236  k config get-clusters

  237  k get namespaces

  238  ls

  239  cd Documents/

  240  ls

  241  mkdir k8s

  242  cd k8s/

  243  docker ps

  244  cd Documents/

  245  ls

  246  cd k8s/

  247  ls

  248  kubectl get nodes

  249  docker ps

  250  docker ps -a

  251  docker ps

  252  minikube start

  253  helm repo add bitnami https://charts.bitnami.com/bitnami

  254  curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null

  255  minikube status

  256  ls

  257  go version

  258  cd Downloads/

  259  ls

  260  tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz

  261  tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz 

  262  sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz 

  263  clear

  264  export PATH=$PATH:/usr/local/go/bin

  265  go version

  266  cd /usr/local/go/bin

  267  ls

  268  export PATH=$PATH:/usr/local/go/bin

  269  exit

  270  go mod init hello.go 

  271  cat go.mod 

  272  go build hello.go 

  273  ls

  274  ./hello 

  275  go version

  276  sudo export PATH=$PATH:/usr/local/go/bin

  277  export PATH=$PATH:/usr/local/go/bin

  278  ls

  279  go version

  280  cd Downloads/

  281  ls

  282  cd

  283  cd Documents/

  284  ls

  285  mkdir go-app

  286  cd go-app/

  287  code .

  288  ls

  289  Cd Documents/

  290  cd Documents/

  291  ls

  292  cd DevOps-tutorial/

  293  ls

  294  cd ..

  295  https://github.com/spring-projects/spring-petclinic.git

  296  git clone https://github.com/spring-projects/spring-petclinic.git

  297  ls

  298  cd spring-petclinic/

  299  ls

  300  java --version

  301  mvn --version

  302  javac --version

  303  mvn compile

  304  mvn package

  305  java -jar target/spring-petclinic-3.3.0-SNAPSHOT.jar 

  306  mvn test

  307  code .

  308  java -jar target/spring-petclinic-3.3.0-SNAPSHOT.jar 

  309  java -jar target/spring-petclinic-3.3.0-SNAPSHOT.jar --httpPort=9001

  310  ls

  311  cd Documents/

  312  ls

  313  git clone https://github.com/mir-owahed/Task-Master-Pro.git

  314  ls

  315  cd Task-Master-Pro/

  316  ls

  317  mvn compile

  318  mvn test

  319  mvn package

  320  ls

  321  cd target/

  322  ls

  323  java -jar todo-app-1.0-SNAPSHOT.jar 

  324  ls

  325  cd Documents/

  326  git clone https://github.com/iam-veeramalla/go-web-app.git

  327  ls

  328  cd go-web-app/

  329  ls

  330  go run main.go 

  331  go version

  332  curl https://go.dev/dl/go1.22.5.linux-amd64.tar.gz

  333  wget https://go.dev/dl/go1.22.5.linux-amd64.tar.gz

  334  ls

  335  sudo rm -rf /usr/local/go

  336  sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz

  337  export PATH=$PATH:/usr/local/go/bin

  338  go version

  339  exit

  340  go version

  341  export PATH=$PATH:/usr/local/go/bin

  342  go version

  343  sudo export PATH=$PATH:/usr/local/go/bin

  344  go version

  345  sudo nano .bashrc

  346  go version

  347  ls

  348  cd Documents/

  349  ls

  350  cd go-web-app/

  351  ls

  352  rm go1.22.5.linux-amd64.tar.gz 

  353  ls

  354  go run main.go 

  355  cd Documents/

  356  ls

  357  git clone https://github.com/jaiswaladi246/Boardgame.git

  358  ls

  359  cd Boardgame/

  360  code .

  361  ls -la

  362  mvn compile

  363  mvn test

  364  mvn package

  365  ls

  366  cd target/

  367  ls

  368  java -jar database_service_project-0.0.4.jar 

  369  cd ..

  370  ls

  371  ls -la

  372  javac -version

  373  ls

  374  docker build -t board-game-app:latest .

  375  sudo docker build -t board-game-app:latest .

  376  docker version

  377  docker pull eclipse-temurin:17-jdk-jammy

  378  docker pull hello-world

  379  docker pull eclipse-temurin:17-jdk-jammy

  380  docker build -t board-game-app:latest .

  381  ls

  382  docker images

  383  docker run --rm -p 8080:8080 board-game-app:latest

  384  docker images

  385  docker ps

  386  docker stop 061cc174c6c9

  387  docker run --rm -d -p 8080:8080 board-game-app:latest

  388  docker ps

  389  docker stop db9645b5c834

  390  docker run --rm -p 8080:8080 board-game-app:latest

  391  docker ps

  392  nano Dockerfile 

  393  docker ps

  394  cd Downloads/

  395  cd ..

  396  ls 

  397  cd Documents/

  398  ls

  399  node

  400  nodejs --version

  401  cd Documents/

  402  ls

  403  git clone https://gitlab.com/mir-owahed/freecodecamp-gitlab-ci.git

  404  ls

  405  cd freecodecamp-gitlab-ci/

  406  ls

  407  code .

  408  cd Documents/

  409  ls

  410  cd freecodecamp-gitlab-ci/

  411  ls

  412  yarn --version

  413  npm --version

  414  node -v

  415  npm install --global yarn

  416  yarn --version

  417  yarn

  418  yarn test

  419  yarn run

  420  yarn start

  421  yarn build

  422  ls

  423  cd build/

  424  ls

  425  cd ..

  426  yarn global add serve

  427  serve -s build

  428  snap install serve

  429  sudo snap install serve

  430  serve -s build

  431  history

  432  history > commands.txt

  433  ls

  434  cd Documents/

  435  ls

  436  cd freecodecamp-gitlab-ci/

  437  ls

  438  yarn test

  439  yarn build

  440  yarn global add serve

  441  serve -s build

  442  yarn start

  443  code .

  444  yarn eject

  445  yarn lint

  446  code .

  447  yarn build

  448  java --version

  449  javac -version

  450  mvn --version

  451  ls

  452  cd Downloads/

  453  ls

  454  unzip helloApp.zip 

  455  ls

  456  cd helloApp/

  457  code .

  458  ls

  459  mvn compile

  460  code .

  461  mvn compile

  462  ls

  463  cd target/

  464  ls

  465  cd ..

  466  code .

  467  mvn test

  468  mvn validate

  469  mvn test

  470  java compile

  471  ls

  472  java compile

  473  ls

  474  mvn compile

  475  mvn test

  476  mvn -X test

  477  mvn compile

  478  mvn package

  479  mvn test

  480  ls

  481  code .

  482  mvn test

  483  mvn -e test

  484  mvn compile

  485  mvn test

  486  mvn clean package

  487  cd target/

  488  ls

  489  cd ..

  490  java -jar target/helloApp-0.0.1-SNAPSHOT.war 

  491  mvn test

  492  exit

  493  ls

  494  cd Downloads/

  495  ls

  496  cd helloApp/

  497  ls

  498  mvn install

  499  java -jar target/helloApp-0.0.1-SNAPSHOT.war 

  500  ls

  501  cd ..

  502  ls

  503  cd helloApp/

  504  ls

  505  mvn test

  506  mvn clean package

  507  cd ..

  508  git clone https://github.com/DSpace/DSpace.git

  509  ls

  510  cd DSpace/

  511  ls

  512  code .

  513  ls

  514  ls -la

  515  mvn validate

  516  mvn compile

  517  mvn install -DskipUnitTests=false -DskipIntegrationTests=false

  518  mvn test -DskipUnitTests=false

  519  ant

  520  sudo apt  install ant

  521  wget https://github.com/DSpace/DSpace/archive/refs/tags/dspace-7.6.2.zip

  522  unzip dspace-7.6.2.zip 

  523  ls

  524  mvn compile

  525  mvn package

  526  cd

  527  ls

  528  docker ps -a

  529  docker ps -aq | xargs docker stop | xargs docker rm

  530  docker ps -a

  531  docker compose version

  532  docker compose -f docker-compose.yml -f docker-compose-cli.yml pull

  533  docker compose -f docker/docker-compose.yml pull

  534  docker compose -f docker/docker-compose.yml -f docker/docker-compose-rest.yml pull

  535  ls

  536  git clone https://github.com/DSpace/dspace-angular.git

  537  ls

  538  cd dspace-angular

  539  git checkout main

  540  npm -v

  541  yarn --version

  542  yarn install

  543  yarn start

  544  cd Downloads/

  545  ls

  546  history

  547  cd helloApp/

  548  ls

  549  history 

  550  code .

  551  mvn clean package

  552  java -jar target/helloApp-0.0.1-SNAPSHOT.war 

  553  history 

  554  netstat -lnp

  555  cd

  556  history

  557  ls

  558  git clone https://github.com/spring-guides/gs-spring-boot.git

  559  cd Downloads/

  560  git clone https://github.com/spring-guides/gs-spring-boot.git

  561  cd gs-spring-boot/

  562  ls

  563  cd complete/

  564  lsssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssl

  565  s

  566  ls

  567  mvn validate

  568  mvn compile

  569  mvn test

  570  mvn package

  571  ls

  572  cd target/

  573  ls

  574  cd ..

  575  java -jar target/spring-boot-complete-0.0.1-SNAPSHOT.jar 

  576  ls

  577  cd ..

  578  code .

  579  cd initial/

  580  ls

  581  mvn validate

  582  mvn compile

  583  mvn test

  584  mvn package

  585  java -jar target/spring-boot-initial-0.0.1-SNAPSHOT.jar 

  586  ls

  587  code .

  588  cd ..

  589  ls

  590  cd complete/

  591  ls

  592  code .

  593  ls

  594  git clone

  595  git clone https://github.com/mir-owahed/nodejs-1st-code.git

  596  cd nodejs-1st-code/

  597  ls

  598  npm install

  599  code .

  600  node app.js 

  601  code .

  602  ls

  603  terraform

  604  ls

  605  cd Documents/

  606  ls

  607  mkdir terraform

  608  cd terraform/

  609  s

  610  ls

  611  terraform --help

  612  sudo apt update

  613  wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

  614  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

  615  sudo apt update && sudo apt install terraform

  616  terraform --help

  617  wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

  618  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

  619  sudo apt update && sudo apt install terraform

  620  sudo dpkg --configure -a

  621  terraform --help

  622  sudo apt update && sudo apt install terraform

  623  apt --fix-broken install

  624  sudo apt --fix-broken install

  625  terraform --help

  626  cd /opt/

  627  sudo mv ~/Downloads/terraform_1.9.5_linux_amd64.zip /opt/

  628  ls

  629  sudo unzip terraform_1.9.5_linux_amd64.zip 

  630  ls

  631  chmod +x terraform

  632  sudo chmod +x terraform

  633  ls

  634  ./terraform 

  635  ls

  636  cd

  637  terraform --help

  638  export PATH=$PATH:/opt/

  639  terraform --help

  640  terraform

  641  terraform --help

  642  cd /opt/

  643  ls

  644  ls -la

  645  terraform --help

  646  ./terraform

  647  export PATH=$PATH:/opt/

  648  cd

  649  terraform --help

  650  export PATH=$PATH:/opt/terraform

  651  terraform --help

  652  terraform --version

  653  ls

  654  cd Documents/

  655  ls

  656  cd terraform/

  657  ls

  658  terraform --help

  659  cd

  660  ls

  661  wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

  662  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

  663  sudo apt update && sudo apt install terraform

  664  terraform --help

  665  code .

  666  npm install --global yarn

  667  yarn --version

  668  GIT_USER=mir-owahed yarn deploy

  669  yarn -v

  670  node -v

  671  yarn install

  672  git status

  673  git add .

  674  git commit -m "yarn.lock added"

  675  git remote -v

  676  git push -u origin main

  677  history

  678  ls

  679  git status

  680  git add .

  681  git commit -m "title edited from local repo"

  682  git push -u origin main

  683  git fetch git@github.com:mir-owahed/tech-with-mir.git

  684  ls

  685  git log

  686  git status

  687  git push -u origin main

  688  git config --global --get user.name

  689  git config --global --get user.email

  690  git remote -v

  691  git status

  692  git commit -am "long blog post updated"

  693  git status

  694  git push

  695  git status

  696  git commit -am "email edited"

  697  git status

  698  git push

  699  git fetch

  700  git status

  701  yarn

  702  npx docusaurus start

  703  ls

  704  cd Documents/

  705  ls

  706  cd tech-with-mir/

  707  ls

  708  cd tech-with-mir/

  709  code .

  710  python --version

  711  sudo apt install python3 python3-pip build-essential python3-dev 

  712  python --version

  713  python3 -V

  714  python3 test.py 

  715  ls

  716  mkdir python-learn

  717  cd python-learn/

  718  code .

  719  python3 test.py 

  720  ls 

  721  cd python-learn/

  722  code .

  723  cd python-learn/

  724  code .

  725  aws --version

  726  terraform init

  727  terraform plan

  728  terraform init

  729  terraform init

  730  terraform fmt

  731  terraform init

  732  terraform fmt

  733  terraform init

  734  code .

  735  cd

  736  ls

  737  cd terraform-eks

  738  code .

  739  git add .

  740  git commit m "spot instances added"

  741  git push

  742  git status

  743  git add .

  744  git commit m "spot instances updated"

  745  git push

  746  git remote -v

  747  git add .

  748  terraform --version

  749  terraform init

  750  terraform validate

  751  terraform fmt

  752  terraform plan

  753  git init

  754  terraform add .

  755  git add .

  756  git commit -m "tf config for aws vpc and ec2"

  757  git branch -M main

  758  git remote add origin git@github.com:mir-owahed/terraform-learn.git

  759  git push -u origin main

  760  code .

  761  python -V

  762  wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh

  763  cd ..

  764  mkdir -p ~/miniconda3

  765  wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh

  766  bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3

  767  rm ~/miniconda3/miniconda.sh

  768  source ~/miniconda3/bin/activate

  769  conda

  770  ls

  771  python -V

  772  conda deactivate

  773  history

  774  history > commands-05-02-25.txt
```
