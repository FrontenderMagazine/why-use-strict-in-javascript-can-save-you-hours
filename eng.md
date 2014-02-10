*Thanks for the feature in the [JavaScript Weekly issue #167 (2th time)][1]*

"use strict" is such a nice feature in JavaScript and is easy to get started!

## How to use {#howtouse}

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
    

## Benefits {#benefits}

## Duplicate keys in object {#duplicatekeysinobject}

    var zombie = {
        eyeLeft : 0,
        eyeRight: 1,
        // ... a lot of keys ...
        eyeLeft : 1
    }
    

This will result in an error because `eyeLeft` key exists twice. This saves you
from wrongly assigning the left eye to the zombie.

## Variables without `var`  {#variableswithoutvar}

    plane = 5;
    

You already know the pain of forgetting to add the `var` keyword before
defining a variable. If you don't then you have to know it's very painfull and 
hard to debug because the variable is defined in the global context and can be 
changed by other parts of the program.  
Imagine a variable `i` globally defined. This can mess up nested loops in the
whole application.

## Duplicate arguments {#duplicatearguments}

    function run(fromWhom, fromWhom){}
    

Notice the `fromWhom` argument exists twice, therefore an error is thrown.

What can happen:

    function run(fromWhom, fromWhom){alert(fromWhom)}
    run(1, 2);
    // alert: 2
    

## Freezes the `arguments` of the functions {#freezestheargumentsofthefunctions
}

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
    

How counter-intuitive is that a change to the arguments (
`arguments[0] = 'alien'`) changes the named argument `fromWhom`? `"use strict"`

> How a small string can save you hours in JavaScript <http://t.co/frkaShxtTW>
>[#JavaScript][2] [#useStrict][3]— Pro JavaScript (@ProJavaScript) 
> 
> [February 6, 2014][4] 
## Your word {#yourword}

**[WoollyMittens][5], reddit user:** has suggested in a [comment][6] 

> In combination with this install a "linter" to catch silly mistakes before
> you even run the code:
><http://www.jshint.com/>   
> Most text editors have plugins for this. Think of it as the wavy red lines
> underneath your spelling mistakes when you write an email, only for code.
>

Soon I will explain how to make it automatic with a grunt task.

**[loz220][7], reddit user:** has suggested in a [comment][6] 

> nice write up. For the [full list of what "use strict" does, click here.][8]
>

## Further reading {#furtherreading}<footer class="article\_meta\_magnum">

 Posted on  <time class="date_magnum" datetime="2014-02-06">Thursday 06 Feb
2014</time></footer>

 [1]: http://javascriptweekly.com/issues/167
 [2]: https://twitter.com/search?q=%23JavaScript&src=hash
 [3]: https://twitter.com/search?q=%23useStrict&src=hash
 [4]: https://twitter.com/ProJavaScript/statuses/431487194750918656
 [5]: http://www.reddit.com/user/WoollyMittens

 [6]: http://www.reddit.com/r/javascript/comments/1x728r/how_a_small_string_can_save_you_hours_in/
 [7]: http://www.reddit.com/user/loz220

 [8]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode