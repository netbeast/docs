# How to develop applications and plugins

To launch and debug you need to have the Dashboard installed. Also it comes with a few set of actions to help you bootstrap your app and debug it.

## Installation

If you previously installed **Netbeast Dashboard** using `npm install -g netbeast-cli`, you already have it available. However if you are going to write apps, it is more comfortable to have it available as a repo:

```
git clone https://github.com/netbeast/dashboard
cd dashboard
npm install # dependencies
npm link # activate the command line actions
```

Below you can find a reference to the actions you can perform with the Dashboard. If you are ready to start developing we can get started right away.

## Dashboard actions

### netbeast new

`netbeast new|create [options] <app>`

Scaffolds a basic app or plugin structure.
Options:

* `--plugin` Creates a basic plugin structure instead of an app structure.

### netbeast start

`netbeast start [options]`

Launches Netbeast. Options:

* `-p, --port <number>` Port to start Netbeast in (http server).
* `-sp, --secure_port <number>` Secure port to start Netbeast in (https server).

### netbeast scan

`netbeast scan|discover`

Finds devices running Netbeast in the local network and displays their IP addresses.

### netbeast install

`netbeast install <file> [host]`

Uploads and installs an app to a remote device running Netbeast.

### netbeast uninstall

`netbeast uninstall <app>`

Uninstalls an application.

### netbeast launch

`netbeast launch <app>`

Launches an application previously installed in Netbeast.

### netbeast stop

`netbeast stop <app>`

Stops an application running in Netbeast.

### netbeast restart

`netbeast restart <app>`

### Other commands

Restarts an application running in Netbeast.

`netbeast forget`

Resets the Dashboard's configuration.

`netbeast -V, --version`

Outputs Netbeast's version number.

`netbeast -h, --help``

Prints this help.




