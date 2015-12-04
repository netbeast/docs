# Methods

### Arguments

Each device can support specific parameters. 
Bridge or Switch can be switched on or off. If you try to set an unsupported parameter to a switch (for example the brightness, `beast('lights').set({bri: 100}))` you will return a soft error. The process keep working but send you a warning.

Here is a list of supported arguments for each device.
*   switch & bridge
    * power `true || false`
*   Bulbs
    * power:        `true || false`
    * brightness:   `0..100`
    * hue:          `0..360`
    * saturation:   `0..100`
    * color:    `{r: 0, b: 0, g: 0} || CC00AA` // Will be translated to hue and saturation

A example of use:
````javascript
var beast = require('netbeast')
beast.resources('lights').set({on: true, bri: 80, hue: 0, sat: 100})
````
 If you have white and color bulbs, the first ones are going to switch on and change the brightness. The color bulbs will also change their color to red and the execution continues without problems.


### Output

All the methods act as a promise and they always return a Javascript object if successful or an error object else.
