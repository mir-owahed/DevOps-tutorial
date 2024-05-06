# Connecting Local Git Repository to GitHub: HTTPS and SSH
From your GitHub account, go to Settings → Developer Settings → Personal Access Token → Generate New Token (Give your password) → Fillup the form → click Generate token → Copy the generated Token, it will be something like ghp_sFhFsSHhTzMDreGRLjmks4Tzuzgthdvfsrta
```
git config credential.helper store

git remote add origin https://github.com/mir-owahed/git-test.git
git branch -M main
git push -u origin main
```
Reference: (https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
