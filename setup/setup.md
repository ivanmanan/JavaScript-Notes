# Setting Up Express Stack

## Initialize Express
$ npm install express --save
$ npm install express-generator -g
$ express <REPO>
$ cd <REPO>
$ npm install

## Initialize Git Repo
$ git init
$ git add .
$ git commit -m "First commit"
### Go to github.com/username
### Copy remote repository URL
$ git remote add origin <REPO URL>
$ git remote -v
$ git branch --set-upstream-to=origin/master master
$ git pull --allow-unrelated-histories
$ git push origin master

## Set-up Server
$ mv app.js server.js
$ nano server.js

### copy and paste files:
$ mv views/index.jade views/home.html
  express/server.js --> repo/
  express/index.js  --> repo/routes/
  express/home.html --> repo/views/
  express/error.html --> repo/views/
  express/config.js --> repo/config.js

### Set-up html view engine
$ npm install ejs

## Setting up MySQL Connection to Express
$ npm install mysql
### Set-up localhost password for mysql
$ sudo apt-get install mysql-server

## Setting up .gitignore
$ nano .gitignore
put in 'config.js' into the file

## Setting up Bootstrap
$ npm install bootstrap@3

## Run on localhost:5000
$ npm start
