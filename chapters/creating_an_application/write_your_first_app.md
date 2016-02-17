# Write your first app
## Eat the dessert first :cake:
First we will install the netbeast SDK. Open a terminal and type:
```
npm install -g netbeast-cli
netbeast new myapp
```

A new folder named _myapp_ will contain some code scaffolded.

Run the following code:
```
cd myapp; node index.js --port 3000 # To have it running on http://localhost:3000
```

And you are done! :fireworks:. Now you can open your favourite editor on such project and start developing.

## OK. Now let's do this slowly :coffee:
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
```json
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

```javascript
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

_ If you rather like to using semicolons in JS go type them! But they [are](https://github.com/feross/standard) [not](http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding) [necessary](http://inimino.org/~inimino/blog/javascript_semicolons), [really](https://www.youtube.com/watch?v=gsfbh17Ax9I)!_

See the _shebang_? (First line of the script `#!/usr/bin/env node`) It is used to tell the Netbeast which interpreter to use when launching and app. **Use this line to indicate node.**

**It is mandatory for `main` to be and executable file.** So if you are writing your app from draft make sure it can be executed:
```
chmod +x server.js
```
As you can see in the code, **the runnable must accept the port by parameter**, so in the case of a webapp they can all be opened from the [Dashboard](https://github.com/netbeast/dashboard).

In order to do that we use [minimist](https://www.npmjs.com/package/minimist), but you can use whatever command parser you prefer. [Commander](https://www.npmjs.com/package/commander) is another recommendation. But you can go hard and parse it in [plain javascript](https://docs.nodejitsu.com/articles/command-line/how-to-parse-command-line-arguments).
```
var argv = require('minimist')(process.argv.slice(2))
port = argv.port || 31416
```

[Express](http://expressjs.com/) is a http node lightweight+unopinated framework. Is really popular software that you may feel handy in the future.

**You will need to install both packages** for the app to work. It will populate the node_modules folder as you can see up in the folder tree. Run:
```
npm install express minimist
```

**We are almost ready to roll!**
`index.html` is a simple user interface that welcomes you as the great developer you are!

```html
<!DOCTYPE html>
<html>
<head>
	<title>xway | get-started</title>
</head>
<style type="text/css">
	body {
		font-family: arial;
	}
</style>
<body>
	<!-- index.html, an optional user interface :] -->
	<h1>
		Hello Netbeast community! <a style="color: red">&#9829;</a>
	</h1>
</body>
</html>
```

_A UI is not strictly needed. There are multiple ways to interact with the user in Netbeast ecosystem as notifications, touchscreens or native mobile apps (docs for these chapters are yet pending, you can request them in [github issues](https://github.com/netbeast/dashboard/issues))._

**Now you can launch it**
Try and debug it locally. Type:
```
./server.js --port 8000
```
And if everything has been good you will be able to open a browser at http://localhost:8000 and see:

![hello netbeast community](../../img/hello_netbeast_community.png)
