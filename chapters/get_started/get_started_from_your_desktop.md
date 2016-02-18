# Install Node.js

All platforms https://nodejs.org/en/download/

```bash
# Mac
brew install node

# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian or Raspberry, as root
curl -sL https://deb.nodesource.com/setup_4.x | bash -
apt-get install -y nodejs
```

### npm

Once you install Nodejs, npm is included.

# Install SDK

### Through npm
``` bash
npm install -g netbeast-cli
```
Now you will be able to run it typing:

```bash
beast start
```

Dashboard will be started on port 8000 unless you run something like:
```
beast start --port 3000
```

### Cloning from **git** repo
```bash
git clone https://github.com/netbeast/dashboard/ && cd dashboard
npm i # by default, dependencies are ignored, so must be installed
./index.js --port 8000
```

And visiting http://localhost:8000...

![Demo Dashboard](../../img/general_demo.gif)
