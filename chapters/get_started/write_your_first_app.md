# Write your first app


### Eat the dessert first
First we will install the netbeast SDK. Open a terminal and type:
```
npm install -g netbeast-cli
netbeast new myapp
```

A new folder named "myapp" will contain some code scaffolded.

Run:
```
cd myapp; node index.js --port 3000
```
To have it running on http://localhost:3000

Now you can open your favourite editor on such project and start developing.

### Let's do this slowly
Every Netbeast app is simply a npm package. For advanced developers you may write your app in python or compile and executable for Netbeast-ready platforms. But for the moment let us focus on the Javascript app itself.

Let us create our first project from scratch. Open a terminal and type:
```
mkdir myapp
cd myapp
atom .
```
Or simply create a new folder with such name and open it in your favourite editor. [Atom](https://atom.io/) or [Sublime](http://www.sublimetext.com/) are ours.

**A basic Netbeast app looks like this:**
```
.
├── index.html
├── node_modules
│   ├── express
│   └── minimist
├── package.json
└── server.js

```
package.json is the information needed by npm to maintain a module into their repositories, analyze dependencies and establish some development workflow.

Netbeast will make use of this file to reduce the overhead of configuration needed to get up and running. It will look for the `main`field in order to launch and executable. For this app:
```
{
    "name":"myapp",
    "version": "1.0.0",
    "description":" A repo with code about how to make simple Netbeast apps.",
    "main": "server.js",
    "dependencies": {
        "express": "^4.12.3", 
        "minimist":"^1.1.0"
    }, 
    "devDependencies":{},
    "scripts":{ 
        "test":"node server.js --port 31416",
        "start": "node server.js"
    },
    "repository": { 
        "type":"git", 
        "url":"https://github.com/netbeast-co/get-started"
    },
    "keywords": [ "iot","netbeast","netbeast.co"],
    "author": "jesus@netbeast.co",
    "license": "GPL 2",
    "bugs": {
        "url":"https://github.com/netbeast-co/get-started/issues"
    },
    "homepage":"https://github.com/netbeast-co/get-started"
}

```

**Let's create your own one to be like this one.** Open a terminal and type:
```
npm init    # And fill the gaps!
```
Or open a file named `package.json` in your editor and copy-paste de code above

We specified in the package that `server.js`is our main file. Let's write a simple HTTP server.
```
#!/usr/bin/env node

/* Requires node.js libraries */
var express = require('express')
var app = express()

// Netbeast apps must accept the port to launch a HTTP server.
var argv = require('minimist')(process.argv.slice(2))
port = argv.port || 31416

if(isNaN(port)) {
	console.log("Port \"%s\" is not a number.", port)
	process.kill(1)
}

app.use(express.static(__dirname))

var server = app.listen(port, function () {
  console.log('Example app listening at http://%s:%s', 
  	server.address().address,
  	server.address().port)
})
```
If you rather like to using semicolons in JS go type them! But they are not   (necessary)[http://inimino.org/~inimino/blog/javascript_semicolons], [really](https://www.youtube.com/watch?v=gsfbh17Ax9I)!

**It is mandatory for `main` to be and executable file.** So if you are writting your app from draft make sure it can be executed:
```
chmod +x server.js
```

Like for this document as well as for others you can suggest new features at [github issues](https://github.com/netbeast/dashboard/issues) or our gitter chat.

![gitter chat](https://badges.gitter.im/Join%20Chat.svg)