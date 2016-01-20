# Methods

### Arguments

Each device can support specific parameters. 
Bridge or Switch can be switched on or off. If you try to set an unsupported parameter to a switch (for example the brightness, `beast('lights').set({brightness: 100}))` you will return a soft error. The process keep working but send you a warning.

Here is a list of supported arguments for each **topic**.
*   switch & bridge
    * power `true || false`
*   lights
    * power:        `true || false`
    * brightness:   `0..100`
    * hue:          `0..360`
    * saturation:   `0..100`
    * color:    `{r: 0, b: 0, g: 0} || CC00AA` // Will be translated to hue and saturation
*   sound
    * volume:       `0..100`
    * status:       `play || pause || stop || mute || unmute || info`  
    * track: `must be the url of the song`

A example of use:
````javascript
var beast = require('netbeast')
beast.resources('lights').set({power: true, brightness: 80, hue: 0, saturation: 100})
````
 If you have white and color bulbs, the first ones are going to switch on and change the brightness. The color bulbs will also change their color to red and the execution continues without problems.


### Output

All the methods act as a promise and they always return a Javascript object if successful or an error object else.
