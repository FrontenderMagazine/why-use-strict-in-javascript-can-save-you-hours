# Why "use strict" in JavaScript can save you hours

"use strict" is such a nice feature in JavaScript and is easy to get started!

## How to use

    // file.js
    "use strict"
    function doStuff(){
    // use strict is enabled here!
    }

By doing this your file.js will "use strict".

If you just want to enable only within a function:

    // file.js
    function a(){
    "use strict";
    // use strict is enabled in this context
    function nestedFunction(){
    // and here too
    }
    }

## Benefits

### Duplicate keys in object

    var zombie = {
    eyeLeft : 0,
    eyeRight: 1,
    // ... a lot of keys ...
    eyeLeft : 1
    }

This will result in an error because `eyeLeft` key exists twice. This saves you
from wrongly assigning the left eye to the zombie.

### Variables without `var`

    plane = 5;

You already know the pain of forgetting to add the `var` keyword before defining
a variable. If you don't then you have to know it's very painfull and hard to
debug because the variable is defined in the global context and can be changed
by other parts of the program.

Imagine a variable `i` globally defined. This can mess up nested loops in the
whole application.

### Duplicate arguments

    function run(fromWhom, fromWhom){}

Notice the `fromWhom` argument exists twice, therefore an error is thrown.

What can happen:

    function run(fromWhom, fromWhom){alert(fromWhom)}
    run(1, 2);
    // alert: 2

### Freezes the `arguments` of the functions

    var run = function(fromWhom){
    arguments[0] = 'alien';
    alert(fromWhom);
    }
    run('zombie');
    // alert: 'alien';

Now if you `"use strict"`

    var run = function(fromWhom){
    "use strict";
    arguments[0] = 'alien';
    alert(fromWhom);
    }
    run('zombie');
    // alert: 'zombie';

How counter-intuitive is that a change to the arguments (`arguments[0] =
'alien'`) changes the named argument `fromWhom`? `"use strict"` saves the day
again.

<blockquote class="twitter-tweet" lang="en"><p>How a small string can save you hours in JavaScript <a href="http://t.co/frkaShxtTW">http://t.co/frkaShxtTW</a> <a href="https://twitter.com/search?q=%23JavaScript&amp;src=hash">#JavaScript</a> <a href="https://twitter.com/search?q=%23useStrict&amp;src=hash">#useStrict</a></p>&mdash; Pro JavaScript (@ProJavaScript) <a href="https://twitter.com/ProJavaScript/statuses/431487194750918656">February 6, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>