# How to install nodejs and npm
```
# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Close the terminal and again open terminal

# download and install Node.js (you may need to restart the terminal)
nvm install 20
or
nvm install node

# verifies the right Node.js version is in the environment
node -v # should print `v20.14.0`

# verifies the right NPM version is in the environment
npm -v # should print `10.7.0`

# Yarn install via npm
npm install --global yarn
yarn --version
```
### Run the code
```
npm init
node app.js
npm install
npm install express --no-save
npm install
node app.js
npm install express
```
```
npm run build
npm start
```
```
git clone https://gitlab.com/mir-owahed/freecodecamp-gitlab-ci.git

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
```
Reference:
1. <http://expressjs.com/en/starter/installing.html>
2. <http://expressjs.com/en/starter/hello-world.html>
3. <https://yarnpkg.com/cli/>


Create React app
```
npm create vite@latest
cd vite-project
npm install
npm run dev
npm run build (it creates Dist folder)
ls
```




### Install & Update Script

To install or update nvm, you should run the install script. To do that, you may either download and run the script manually, or use the following cURL or Wget command:
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```
or
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```
To verify
```
command -v nvm
```

Usage

To download, compile, and install the latest release of node, do this:
```
nvm install node # "node" is an alias for the latest version
```
To install a specific version of node:
```
nvm install 14.7.0 # or 16.3.0, 12.22.1, etc
```
To install npm
```
nvm install-latest-npm
```
Reference:
1. <https://nodejs.org/en/download/package-manager/>
2. <https://github.com/nvm-sh/nvm?tab=readme-ov-file#usage>

