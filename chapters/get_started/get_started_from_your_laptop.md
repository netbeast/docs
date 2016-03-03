#Netbeast on your Laptop

Be ready to start using Netbeast on your Laptop :rocket:

### 1. Install Node.js

Choose your package. Node.js is available for all platforms in https://nodejs.org/en/download/


> But, I want to do it through the command line:

```bash
1.b. Mac
brew install node

1.c. Using Ubuntu
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs

1.d Using Debian or Raspberry, as root
curl -sL https://deb.nodesource.com/setup_4.x | bash -
apt-get install -y nodejs
```

### 2. Install npm

Once you install Nodejs, npm is included. :white_check_mark:

### 3. Install Netbeast SDK

#### 3.a. Through npm
``` bash
npm install -g netbeast-cli
```
After it finishes you will be able to run it typing:

```bash
netbeast start
```

Dashboard will be started on port 8000 unless you run something like:
```
netbeast start --port 3000
```

Run with _help_ to get all options:
```
netbeast --help
```

#### 3.b Cloning from **git** repo
```bash
git clone https://github.com/netbeast/dashboard/ && cd dashboard
npm i # by default, dependencies are ignored, so must be installed
./index.js --port 8000
```

###  4. Done! :fireworks:
Now you can visit http://localhost:8000

![Demo Dashboard](../../img/dashboard-demo.gif)

### 5. [Subscribe](http://www.netbeast.co) to Netbeast to have access to the lastest updates

### 6. Go to [First Steps](../first_steps/index.md) to keep learing about Netbeast

