# Create your first plugin

Let's use the sdk to make things faster and try it live.
Click [here](../get_started/install_dashboard.md) if you have not installed it yet.

[watch a preview]

### Create the app skeleton:


```
beast new bulb-plugin
cd bulb-plugin
npm install
```

Open the **bulb-plugin** folder with your favourite editor or IDE.
You should have now a file structure like this:
```
.
├── LICENSE
├── README.md
├── node_modules
│   ├── express
│   ├── minimist
│   └── netbeast
├── package.json
├── public
│   └── index.html
└── server.js
```

Now let's get started. Declare your app as a plugin. Append the following lines to **package.json** before the closing `}` tag.
```
  "netbeast": {
    "type": "plugin"
  }
```

### The hardware
We are going to mimic hardware connection by creating a really simple webapp. For the result below you must copy paste the following code for a new **index.html**:



### The plugin code
For your code to be available for the Netbeast API you must implement HTTP routes. We will implement one for the simplest case:

