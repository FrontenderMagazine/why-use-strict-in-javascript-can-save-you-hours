# Как строгий режим `"use strict"` в JavaScript может сэкономить вам пару часов

Строгий режим (директива `"use strict"`) - очень хорошее явление в JavaScript и 
начать с ним работать очень просто!

## Как его применить

    // file.js
    "use strict"
    function doStuff(){
    // строгий режим активирован!
    }

Если сделать так, в файле `file.js` будет использоваться строгий режим.

Если вы хотите подключить его только внутри функции:

    // file.js
    function a(){
    "use strict";
    // строгий режим активирован для этого контекста
    function nestedFunction(){
    // и для этого тоже
    }
    }

## Преимущества

### Продублированные ключи в объекте

    var zombie = {
    eyeLeft : 0,
    eyeRight: 1,
    // ... много ключей ...
    eyeLeft : 1
    }

В результате получим ошибку, так как ключ `eyeLeft` встречается дважды. Это 
спасает вас от ошибки в присвоении глаза для зомби.

### Переменные без `var`

    plane = 5;

Вы уже знаете какие проблемы возникают если забыть добавить ключевое слово `var` 
в объявлении переменной. Если нет, знайте что отлаживать потом такой код очень 
трудно, ведь переменная объявлена в глобальном контексте и может изменяться 
другими частями программы.

Представьте переменную `i`, объявленную глобально. Это может привести в 
беспорядок все вложенные циклы в приложении.

### Продублированные аргументы

    function run(fromWhom, fromWhom){}

Обратите внимание что аргумент `fromWhom` прописан дважды, потому выводится 
ошибка. 

Что может случиться:

    function run(fromWhom, fromWhom){alert(fromWhom)}
    run(1, 2);
    // alert: 2

### Фиксация `arguments` внутри функции

    var run = function(fromWhom){
    arguments[0] = 'alien';
    alert(fromWhom);
    }
    run('zombie');
    // alert: 'alien';

Если использовать строгий режим

    var run = function(fromWhom){
    "use strict";
    arguments[0] = 'alien';
    alert(fromWhom);
    }
    run('zombie');
    // alert: 'zombie';

Насколько парадоксальным является то, что при изменении аргументов 
(`arguments[0] = 'alien'`) изменяется именованный аргумент `fromWhom`? 
`"use strict"` опять спасает положение.

<blockquote class="twitter-tweet" lang="en"><p>Как короткая строка в JavaScript может сэкономить вам пару часов <a href="http://t.co/frkaShxtTW">http://t.co/frkaShxtTW</a> <a href="https://twitter.com/search?q=%23JavaScript&amp;src=hash">#JavaScript</a> <a href="https://twitter.com/search?q=%23useStrict&amp;src=hash">#useStrict</a></p>&mdash; Pro JavaScript (@ProJavaScript) <a href="https://twitter.com/ProJavaScript/statuses/431487194750918656">Февраль 6, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>