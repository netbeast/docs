# Methods

###Arguments###

Each device can support specific parameters. 
Bridge or Switch can be switched on or off. If you try to set an unsupported parameter to a switch (for example the brightness, .set({bri: 255})) you will return a soft error. The process keep working but send you a warning.

Here is a list of supported arguments for each device.
*   switch & bridge
    * on - true/false
*   Bulbs
    * on    - true/false
    * bri   - 0-255
    * hue   - 0-65535   (color bulbs)
    * sat   - 0-255     (color bulbs)

A example of use:
````javascript
nb.resources('lights').set({on: true, bri: 200, hue: 0, sat: 255})
````
 If you have white and color bulbs, the first ones are going to switch on and change the brightness. The color bulbs will also change their color to red and the execution continues without problems.


###Output###

All the methods act as a promise and they always return a json object like this:
`````
{
    error:  
    data:
}
````