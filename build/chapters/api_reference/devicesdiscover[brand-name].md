# devices.discover([brand-name])

This function allows us to activate the discovery process. With the brand-name parameter you can specify a concrete app (like belkin-wemo, philips-hue). If you don´t include this argument, the discovery will be apply to all available brands.

````javascript
var nb = require('netbeast')

nb.devices().discovery('belkin-wemo')
.then(function (data) {}
.catch(function (error) {}
````