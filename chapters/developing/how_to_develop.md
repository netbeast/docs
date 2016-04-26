# How to develop applications and plugins

To speed up the development process, you can use the Toolbelt to bootstrap the development of both apps and plugins. The Toolbelt is a CLI (Command Line Interface) utility that allows to perform a variety of tasks.

## Installation

If you previously installed Netbeast using npm, you already have the Toolbelt available. Otherwise, type the following to install it:

```bash
  npm install -g netbeast-cli
```

Bellow you can find a reference to the actions you can perform with the Toolbelt. If you are ready to start developing we can get started right away.

## Toolbelt actions

### netbeast new

`netbeast new|create [options] <app>` 

Creates a basic app or plugin structure.
Options:

* `--plugin` Creates a basic plugin structure instead of an app structure.

### netbeast start

`netbeast start [options`

Launches Netbeast. Options:

* `-p, --port <number>` Port to start Netbeast in (http server).
* `-sp, --secure_port <number>` Secure port to start Netbeast in (https server).

### netbeast package

`netbeast package|pkg [options] [app]`

Compresses an app into a tar.gz file.
Options:

* `-o, --to <path>` Outputs to the specified path and filename.

### netbeast unpackage

`netbeast unpackage|unpkg [options] [app]`

Uncompresses a tar.gz file app. Options:

* `-o, --to <path>` Outputs to the specified path and filename.

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

Resets the Toolbelt's configuration.

`netbeast -V, --version`

Outputs Netbeast's version number.

`netbeast -h, --help``

Prints this help.




