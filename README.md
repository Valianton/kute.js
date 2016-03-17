# KUTE.js
A minimal <b>native Javascript</b> tweening engine with <b>jQuery</b> plugin, with most essential options for web developers, designers and animators, delivering easy to use methods to set up high performance, cross-browser animations.

<b>Important</b>: starting with 0.9.5 version, KUTE.js changes the prototype structure for performance, usability and browser support, as well as extensibility. The documentation and examples no longer support old versions prior to 0.9.5 release.

# CDN
Thanks to jsdelivr, we have a CDN link <a target="_blank" href="http://www.jsdelivr.com/#!kute.js">here</a>.

# Demo
For documentation, examples and other cool tips, check the <a href="http://thednp.github.io/kute.js/">demo</a>.

# NPM/Bower
You can install this through NPM or bower respectively:
```
    $ npm install kute.js
    # or
    $ bower install kute.js
```

# CommonJS/AMD support
You can use this module through any of the common javascript module systems. For instance:

```javascript
// NodeJS/CommonJS style
var kute = require("kute.js");
// Add Bezier Easing
require("kute.js/kute-bezier");
// Add Physics Easing
require("kute.js/kute-physics");

// AMD
define([
    "kute.js",
    "kute.js/kute-jquery.js", // optional for jQuery apps
    "kute.js/kute-bezier.js", // optional for more accurate easing functions
    "kute.js/kute-physics.js" // optional for more flexible & accurate easing functions
], function(KUTE){
    // ...
});
```

# Basic Usage
At a glance, you can write one line and you're done.
```javascript
//vanilla js
KUTE.fromTo('selector', fromValues, toValues, options).start();

//with jQuery plugin
var tween = $('selector').KUTE('fromTo', fromValues, toValues, options);
$(tween).KUTE('start');
```

# Advanced Usage
Quite easily, you can write 'bit more lines and you're making the earth go round.
```javascript
//vanilla js is always the coolest
KUTE.fromTo(el,
    { translate: 0, opacity: 1 }, // fromValues
    { translate: 150, opacity: 0 }, // toValues
    
    // tween options object
    { duration: 500, delay: 0, easing	: 'exponentialInOut', // basic options

      // callbacks
      start: functionOne, // run function when tween starts
      complete: functionTwo, // run function when tween animation is finished
      update: functionThree // run function while tween running    
      stop: functionThree // run function when tween stopped    
      pause: functionThree // run function when tween paused    
      resume: functionThree // run function when resuming tween    
    }
).start(); // this is to start animation right away
```

# jQuery Plugin
This aims to make the KUTE.js script work native within other jQuery apps but it's not always really needed as we will see in the second subchapter here. The plugin is just a few bits of code to bridge all of the the awesome `kute.js` methods to your jQuery apps. The plugin can be found in the [/master](https://github.com/thednp/kute.js/blob/master/kute-jquery.js) folder. So let's have a look at the syntax.

## Using the jQuery Plugin
Here's a KUTE.js jQuery Plugin example that showcases most common usage in future apps:
```javascript
// first we define the object(s)
var tween = $('selector').KUTE('fromTo', // apply fromTo() method to selector
  
    { translate: 0, opacity: 1 }, // fromValues
    { translate: 150, opacity: 0 }, // toValues
    
    // tween options object
    { duration: 500, delay: 0, easing	: 'exponentialInOut', // basic options

      //callbacks
      start: functionOne, // run function when tween starts
      complete: functionTwo, // run function when tween animation is finished
      update: functionThree // run function while tween running    
      stop: functionThree // run function when tween stopped    
      pause: functionThree // run function when tween paused    
      resume: functionThree // run function when resuming tween    
    }
);

// then we apply the tween control methods, like start
$(tween).KUTE('start');
```

## Alternative usage in jQuery powered applications
In some cases you can handle animations inside jQuery applications even without the plugin. Here's how the code could look like:
```javascript
var tween = KUTE.fromTo($('selector')[0], fromValues, toValues, options);
tween.start();
```
Pay attention to that `$('selector')[0]` as jQuery always creates an array of selected objects and not a single object, that is why we need to focus a tween object to a single HTML object and not a selection of objects. Selections of objects should be handled with `for() {}` loops if that is the case, while the jQuery Plugin handles this properly for your app, as you would expect it to.


# How it works
* it computes all the values before starting the animation, then caches them to avoid layout thrashing that occur during animation
* handles all kinds of `transform` properties and makes sure to always use the same order of the `transform` properties (`translate`, `rotate`, `skew`, `scale`)
* allows you to set `perspective` for an element or it's parent for 3D transforms
* computes properties' values properly according to their measurement unit (px,%,deg,etc)
* properly handles cross browser 3D `transform` with `perspective` and `perspective-origin` for element or it's parent
* converts `HEX` colors to `RGB` and tweens the numeric values, then ALWAYS updates color via `RGB`
* properly replaces `top`, `centered` or any other background position with proper value to be able to tween
* for most supported properties it reads the current element computed style property value as initial value (via `currentStyle || getComputedStyle`)
* because it can read properties values from previous tween animations, KUTE.js can do some awesome chaining with it's `.to()` method
* allows you to add many callbacks: `start`, `update`, `complete`, `pause`, `stop`, and they can be set as tween options
* since `translate3D` is best for movement animation performance, `kute.js` will always use it
* accepts "nice & easy string" easing functions, like `linear` or `easingExponentialOut` (removes the use of the evil `eval`, making development safer, easier and closer to standards :)
* uses all 31 Robert Penner's easing functions, as well as bezier and physics easing functions
* handles browser prefixes for you for `transform`, `perspective`, `perspective-origin`, `border-radius` and `requestAnimationFrame`
* all this is possible with a core script of less than 20k size!

# Browser Support
Since most modern browsers can handle pretty much everything, legacy browsers need some help, so give them <a href="https://cdn.polyfill.io/v2/docs/">polyfills</a>. I also packed a small polyfill set with most essential features required by KUTE.js to work, it's called [minifill](https://github.com/thednp/minifill), try it.

# Contributions
* Dav aka [@dalisoft](https://github.com/dalisoft) contributed a great deal for the performance and functionality of KUTE.js
* [Ingwie Phoenix](https://github.com/IngwiePhoenix): RequireJS/CommonJS compatibility and usability with common package managers
* Others who [contribute](https://github.com/thednp/kute.js/graphs/contributors) to the project

# License
<a href="https://github.com/thednp/kute.js/blob/master/LICENSE">MIT License</a>