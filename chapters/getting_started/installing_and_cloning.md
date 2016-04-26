# Installing and cloning Netbeast

Get ready. Your journey to simple and seamless IoT development has just began!

## Install Node.js

> Netbeast is tested and guaranteed to support Node.js 0.12.x and later.

**Node.js is available for all platforms** [here](https://nodejs.org/en/download/).

If you want to install Node.js through the command line just type the following:

**Mac OS**
```bash
brew install node
```

**Ubuntu based Linux OS type**
```bash
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
````

**Debian based Linux OS type**
```bash
curl -sL https://deb.nodesource.com/setup_4.x | bash -
apt-get install -y nodejs
```

Please go [here](https://nodejs.org/en/download/package-manager/) to use another package manager.

- Node comes with npm installed so you should have a version of npm. Still, npm gets updated more frequently than Node does, so you'll want to make sure it's the latest version.

```
sudo npm install npm -g
```

Test: ```Run npm -v```. The version should be higher than 2.1.8.

## Install Netbeast

Netbeast is available as a [npm package](https://www.npmjs.com/package/netbeast-cli). To install it just type on a command line:

``` bash
npm install -g netbeast-cli
```

## Run Netbeast

To start Netbeast, type

```bash
netbeast start
```

The Dashboard will start on port 8000 unless you specify another port:
```
netbeast start --port 3000
```

To see all the options for the ```netbeast``` command run
```
netbeast --help
```

## For development - install from github

Running the code from GitHub is only intended for users who are happy to be using development code, or for developers wanting to contribute to the code.

You can clone the source repository directly from GitHub:
```
git clone https://github.com/netbeast/dashboard.git
```

Once cloned, the core pre-requisite modules must be installed:

```
cd dashboard
npm install
```

Now you have all the npm packages installed, run it as follows:

```
npm start
```

##  You made it, huzzah!

Now you can access http://localhost:8000 on a web browser to access the Dashboard.

Note: in case you launched Netbeast on another port you have to specify that port on the URL instead of 8000.

![Demo Dashboard](../../img/dashboard-demo.gif)



