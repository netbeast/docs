#Third party development tools

Netbeast is trying to become compatible with all the third party development tools focused on IoT. Here you will find all we are compatible with. 

Feel free to contribute or suggest any other tool on the [forum](http://forum.netbeast.co)

## Electron

[Electron](http://electron.atom.io/) is a framework for creating native applications with web technologies like JavaScript, HTML, and CSS. It takes care of the hard parts so you can focus on the core of your application.

Netbeast has been adapted to be compiled as desktop application with electron. 

After installing all packages dependencies run:

```
npm run electron
```

#### Compile the desktop version for MACOS

If you want to create the Netbeast dashboard application for mac, follow these steps:

##### 1. Install last Nodejs version (In this example I have v5.7.1) & npm packages

```
# Install electron-packager
npm install -g electron-packager

# Install appdmg
npm install -g appdmg

#Install node-gyp
npm install -g node-gyp

# Clone the Netbeast dashboard
git clone https://github.com/netbeast/dashboard

# Install all dependencies
cd dashboard
npm install
```

- You can find more information about how these packages work: [electron-packager](https://github.com/electron-userland/electron-packager) [appdmg](https://github.com/LinusU/node-appdmg)

- We also recommend having the last version of Nodejs. You can download it from [here](https://nodejs.org/en/)

##### 2. Create the Mac App

```
electron-packager dashboard Netbeast --platform=darwin --arch=x64 --version=0.37.2 --icon=dashboard/electron/icon.icns --version-string.CompanyName=Netbeast --version-string.ProductName=NetbeastDashboard
```

-  Check the electron version ```./node_modules/.bin/electron -v```in my case: 0.37.2

##### 3. Create the Mac dmg

Once you have created the Netbeast dashboard app you can run the following command:


```
cd Netbeast-darwin-x64

#Copy files from dashboard folder to the new one
cp ../dashboard/electron/icon.icns ../dashboard/electron/appdmg.json ../dashboard/electron/background.png .

#Package to .dmg
appdmg appdmg.json ~/Desktop/Netbeast.dmg
```

- Then you will have the Netbeast.dmg file on your desktop :smile:

####Compile the desktop version for Linux

##### 1. Install last Nodejs version (In this example I have v5.7.1) & npm packages

```
# Install electron-packager
npm install -g electron-packager

#Install node-gyp
npm install -g node-gyp

# Clone the Netbeast dashboard
git clone -b electron --single-branch https://github.com/netbeast/dashboard

# Install all dependencies
cd dashboard
npm install
```

##### 2. Create the Linux App

```
electron-packager dashboard Netbeast --platform=linux --arch=all --version=0.37.2 --icon=dashboard/electron/icon.icns --version-string.CompanyName=Netbeast --version-string.ProductName=NetbeastDashboard
```

- The result will be two folders: 
  - Netbeast-linux-ia32 : 32 bits version
  - Netbeast-linux-x64: 64 bits version

Now if you want to run the application go to the folder and double click on "Netbeast" :smile:

#### Compile the desktop version for Windows

##### Building Windows apps from non-Windows platforms

Building an Electron app for the Windows platform with a custom icon requires editing the Electron.exe file. Currently, electron-packager uses node-rcedit to accomplish this. A Windows executable is bundled in that node package and needs to be run in order for this functionality to work, so on non-Windows host platforms, Wine needs to be installed. On OS X, it is installable via Homebrew.

You can find more information [here](https://github.com/electron-userland/electron-packager)

##### Create the Windows App

```
electron-packager dashboard Netbeast --platform=win32 --arch=all --version=0.37.2 --icon=dashboard/electron/icon.ico --version-string.CompanyName=Netbeast --version-string.ProductName=NetbeastDashboard
```

- The result will be two folders: 
  - Netbeast-win32-ia32 : 32 bits version
  - Netbeast-win32-x64: 64 bits version

Now if you want to run the application go to the folder and double click on "Netbeast.exe"

## Node-Red

[Node-RED](http://nodered.org/) is a tool for wiring together hardware devices, APIs and online services in new and interesting ways.

Netbeast has been uploaded as a flow for node-red. Look [here](http://flows.nodered.org/node/node-red-contrib-netbeast)

You can check [this](https://www.toptal.com/nodejs/programming-visually-with-node-red) interesting post about how to start using Netbeast with Node-Red

## Freeboard

[Freeboard](http://freeboard.io) is a web-based tool that allow you to build beautiful, fully-interactive user-interfaces for your connected devices. 

It is available as a Netbeast app. You can check how to start using Freeboard on the following [post](https://netbeast.co/blog/quick-personalized-dashboards-connecting-freeboard-to-netbeast).