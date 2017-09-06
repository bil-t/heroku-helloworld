# heroku-helloworld
A heroku hello world sample walkthrough

# Prerequisites
## Installed the following software
* Heroku Command Line Interface (CLI) 
visit https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up
* Node (version greater than 4)
* Git

## Check your environment
```
set HTTP_PROXY=http://proxy:3128
set HTTPS_PROXY=http://proxy:3128
```

```
> node -v
v6.11.1
```

```
>git --version
git version 2.8.1.windows.1
```

```
> heroku login                      
Enter your Heroku credentials:      
Email: bilal.tayara@murex.com       
Password: *******                   
Logged in as bilal.tayara@murex.com 
```
#Build your first application

## Create application directory
```
mkdir heroku-HelloWorld
cd heroku-HelloWorld
```

## Initialize git repository
```
>git init
Initialized empty Git repository in D:/Dev/heroku-HelloWorld/.git/
```
## Add .gitignore file

```
\# Node build artifacts
node_modules
npm-debug.log

\# Local development
*.env
*.dev
.DS_Store

\# Docker
Dockerfile
docker-compose.yml
```

```
> git add .
> git commit -m 'init'
[master (root-commit) 9c99d7e] 'init'
 2 files changed, 195 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 HelloWorld.md
```
## Initialize your node project

```
> npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (heroku-HelloWorld) hello-node
version: (1.0.0)
description: Sample hello world using node and express
entry point: (index.js) app.js
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to D:\Dev\heroku-HelloWorld\package.json:

{
  "name": "hello-node",
  "version": "1.0.0",
  "description": "Sample hello world using node and express",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this ok? (yes) yes
```

## Install express in the myapp directory
```
> npm install express --save
hello-node@1.0.0 D:\Dev\heroku-HW
`-- express@4.15.4
  +-- accepts@1.3.4
  | +-- mime-types@2.1.17
  | | `-- mime-db@1.30.0
  | `-- negotiator@0.6.1
  +-- array-flatten@1.1.1
  +-- content-disposition@0.5.2
  +-- content-type@1.0.2
  +-- cookie@0.3.1
  +-- cookie-signature@1.0.6
  +-- debug@2.6.8
  | `-- ms@2.0.0
  +-- depd@1.1.1
  +-- encodeurl@1.0.1
  +-- escape-html@1.0.3
  +-- etag@1.8.0
  +-- finalhandler@1.0.4
  | `-- unpipe@1.0.0
  +-- fresh@0.5.0
  +-- merge-descriptors@1.0.1
  +-- methods@1.1.2
  +-- on-finished@2.3.0
  | `-- ee-first@1.1.1
  +-- parseurl@1.3.1
  +-- path-to-regexp@0.1.7
  +-- proxy-addr@1.1.5
  | +-- forwarded@0.1.0
  | `-- ipaddr.js@1.4.0
  +-- qs@6.5.0
  +-- range-parser@1.2.0
  +-- send@0.15.4
  | +-- destroy@1.0.4
  | +-- http-errors@1.6.2
  | | `-- inherits@2.0.3
  | `-- mime@1.3.4
  +-- serve-static@1.12.4
  +-- setprototypeof@1.0.3
  +-- statuses@1.3.1
  +-- type-is@1.6.15
  | `-- media-typer@0.3.0
  +-- utils-merge@1.0.0
  `-- vary@1.1.1

npm WARN hello-node@1.0.0 No repository field.
```

In your favorite text editor create a file named app.js and write the following:

```
var express = require('express');
var port = (process.env.PORT || 3000);
var app = express();
app.get('/', function (req, res) {
  res.send('Hello World!');
});
app.listen(port, function () {
  console.log('Example app listening on port ' + port);
});
```
## Define a Procfile
Heroku uses a Procfile to explicitly declare what command should be executed to start your app.
In your application add a text file named Procfile with the following content:

```
  web: node app.js
```

Add your changes to the local git repository

```
> git add .

> git commit -m "hello world"
```
## Create your app on Heroku

```
> heroku create
Creating app... done, lit-depths-42556
https://lit-depths-42556.herokuapp.com/ | https://git.heroku.com/lit-depths-42556.git
```
## Deploy the app on Heroku
```
> git push heroku master
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (9/9), done.
Writing objects: 100% (10/10), 3.37 KiB | 0 bytes/s, done.
Total 10 (delta 1), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Node.js app detected
remote:
remote: -----> Creating runtime environment
remote:
remote:        NPM_CONFIG_LOGLEVEL=error
remote:        NPM_CONFIG_PRODUCTION=true
remote:        NODE_VERBOSE=false
remote:        NODE_ENV=production
remote:        NODE_MODULES_CACHE=true
remote:
remote: -----> Installing binaries
remote:        engines.node (package.json):  unspecified
remote:        engines.npm (package.json):   unspecified (use default)
remote:
remote:        Resolving node version 6.x...
remote:        Downloading and installing node 6.11.3...
remote:        Using default npm version: 3.10.10
remote:
remote: -----> Restoring cache
remote:        Skipping cache restore (not-found)
remote:
remote: -----> Building dependencies
remote:        Installing node modules (package.json)
remote:        hello-node@1.0.0 /tmp/build_72d57f6a961ddb3204a9911349a4254e
remote:        └─┬ express@4.15.4
remote:        ├─┬ accepts@1.3.4
remote:        │ ├─┬ mime-types@2.1.17
remote:        │ │ └── mime-db@1.30.0
remote:        │ └── negotiator@0.6.1
remote:        ├── array-flatten@1.1.1
remote:        ├── content-disposition@0.5.2
remote:        ├── content-type@1.0.2
remote:        ├── cookie@0.3.1
remote:        ├── cookie-signature@1.0.6
remote:        ├─┬ debug@2.6.8
remote:        │ └── ms@2.0.0
remote:        ├── depd@1.1.1
remote:        ├── encodeurl@1.0.1
remote:        ├── escape-html@1.0.3
remote:        ├── etag@1.8.0
remote:        ├─┬ finalhandler@1.0.4
remote:        │ └── unpipe@1.0.0
remote:        ├── fresh@0.5.0
remote:        ├── merge-descriptors@1.0.1
remote:        ├── methods@1.1.2
remote:        ├─┬ on-finished@2.3.0
remote:        │ └── ee-first@1.1.1
remote:        ├── parseurl@1.3.1
remote:        ├── path-to-regexp@0.1.7
remote:        ├─┬ proxy-addr@1.1.5
remote:        │ ├── forwarded@0.1.0
remote:        │ └── ipaddr.js@1.4.0
remote:        ├── qs@6.5.0
remote:        ├── range-parser@1.2.0
remote:        ├─┬ send@0.15.4
remote:        │ ├── destroy@1.0.4
remote:        │ ├─┬ http-errors@1.6.2
remote:        │ │ └── inherits@2.0.3
remote:        │ └── mime@1.3.4
remote:        ├── serve-static@1.12.4
remote:        ├── setprototypeof@1.0.3
remote:        ├── statuses@1.3.1
remote:        ├─┬ type-is@1.6.15
remote:        │ └── media-typer@0.3.0
remote:        ├── utils-merge@1.0.0
remote:        └── vary@1.1.1
remote:
remote:
remote: -----> Caching build
remote:        Clearing previous node cache
remote:        Saving 2 cacheDirectories (default):
remote:        - node_modules
remote:        - bower_components (nothing to cache)
remote:
remote: -----> Build succeeded!
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote:
remote: -----> Compressing...
remote:        Done: 13.7M
remote: -----> Launching...
remote:        Released v3
remote:        https://lit-depths-42556.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/lit-depths-42556.git
 * [new branch]      master -> master
```
## Open your web app

```
heroku open
```


---------------------------
# WIP
---------------------------

npm install --save --save-exact cool-ascii-faces

edit app.js:

var express = require('express');
var cool = require('cool-ascii-faces');
var port = (process.env.PORT || 3000);
var app = express();
app.get('/', function (request, response) {
  response.send('Hello World! ' + cool());
});
app.listen(port, function () {
  console.log('Example app listening on port ' + port);
});

git add.
git commit -m "add cool faces"
git push heroku master

==============================
heroku addons:create heroku-postgresql:hobby-dev

heroku config

edit package.json 
  "dependencies": {
      ....
      "pg": "6.x"      
  }

npm install


var pg = require('pg');

app.get('/db', function (request, response) {
  pg.connect(process.env.DATABASE_URL, function(err, client, done) {
    client.query('SELECT * FROM test_table', function(err, result) {
      done();
      if (err)
       { console.error(err); response.send("Error " + err); }
      else
       { response.render('pages/db', {results: result.rows} ); }
    });
  });
});
