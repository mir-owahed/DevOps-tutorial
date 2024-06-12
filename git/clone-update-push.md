# clone github repo and update and push 
```
10  su -
sudo visudo
   11  sudo apt update
   12  ls
   13  git clone https://github.com/mir-owahed/DevOps-tutorial.git
   14  sudo apt install git
   15  clear
   16  git clone https://github.com/mir-owahed/DevOps-tutorial.git
   17  ls
   18  cd DevOps-tutorial/
   19  git remote -v
   20  ls
   21  cd programming-basics-learn/
   22  ls
   23  mkdir python-app
   24  cd python-app/
   25  git remote -v
   26  cd
   27  cd DevOps-tutorial/
   28  git status
   29  ls
   30  cd programming-basics-learn/
   31  LS
   32  ls
   33  cd python-app/
   34  nano README.md
   35  cd ..
   36  git status
   37  git add .
   38  git commit -m "python app folder added"
   39  git config --global user.name "Mir Ali"
   40  git config --global user.email bachchu333@gmail.com
   41  git status
   42  git remote -v
   
   45  ssh-keygen
   46  sudo cat /home/mir/.ssh/id_rsa.pub
[copy the pub key and paste it on GitHub pat and generate token]
  
   50  git push
   51  history
```
