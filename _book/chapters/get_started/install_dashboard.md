# Install Dashboard

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

### Set up your Netbeast

Netbeast Dashboard is the main web UX for a next generation router. 

We prepared a <u>very lightweight</u> Raspberry Pi 2 distro with the dashboard already installed</u> to show how this future Netbeast is going to be. It is published every two weeks [here](http://bit.ly/1HjkWo2).

The beta looks like this:

![Demo Dashboard](../../img/general_demo.gif)