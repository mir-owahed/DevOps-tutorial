# Connecting Local Git Repository to GitHub: HTTPS and SSH
From your GitHub account, go to Settings → Developer Settings → Personal Access Token → Generate New Token (Give your password) → Fillup the form → click Generate token → Copy the generated Token, it will be something like ghp_sFhFsSHhTzMDreGRLjmks4Tzuzgthdvfsrta
```
git config credential.helper store
git push -u origin main

git remote add origin https://github.com/mir-owahed/git-test.git
git branch -M main
git push -u origin main
```
Reference: (https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

# connecting-to-github-with-ssh
```
How to clone, push, and pull with git (beginners GitHub tutorial)
ssh-keygen -t ed25519 -C "bachchu333@gmail.com"
ls ~/.ssh/
cd ~/.ssh/
cat .pub
[open github > setting >ssh and gpg]
```
# Clone existing repo and update code and then push to github
```
Preq: ssh setup for github
671  git@github.com:mir-owahed/tech-with-mir.git

  672  git clone git@github.com:mir-owahed/tech-with-mir.git

  673  cd tech-with-mir/

  674  ls

  675  code .



670  yarn -v
  671  node -v
  672  yarn install
  673  git status
  674  git add .
  675  git commit -m "yarn.lock added"
  676  git remote -v
  677  git push -u origin main
  678  history
```
