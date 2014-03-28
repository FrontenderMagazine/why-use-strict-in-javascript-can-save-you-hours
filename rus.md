# Как строгий режим `"use strict"` в JavaScript может сэкономить вам пару часов

Строгий режим (директива `"use strict"`) — очень хорошее явление в JavaScript 
и начать с ним работать очень просто!

## Как его применить

    // file.js
    "use strict"
    function doStuff(){
    	// строгий режим активирован
    }

В описанный выше примере строгий режим применяется по всему коду в файле 
`file.js`.

Если вы хотите подключить его только внутри функции, используйте следующий пример:

    // file.js
    function a(){
        "use strict";
        // строгий режим активирован только для кода внутри функции
        function nestedFunction(){
    		// и будет также применяться внутри вложенной функции
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

В результате мы получим ошибку, так как ключ `eyeLeft` встречается дважды. В данном случае строгий режим спасёт вас от дублирования ключа в объекте.

### Переменные без `var`

    plane = 5;

Наверняка вы уже знаете, какие проблемы могут возникнуть, если забыть добавить 
ключевое слово `var` в объявлении переменной. Если нет, то знайте, что 
отлаживать потом такой код потом весьма затруднительно, ведь подобная 
переменная будет объявлена в глобальном контексте и может изменяться другими 
частями программы.

Только представьте переменную `i`, объявленную глобально. Это может внести 
беспорядок во все вложенные циклы в приложении.

### Продублированные аргументы

    function run(fromWhom, fromWhom){}

Обратите внимание что аргумент `fromWhom` прописан дважды, для данного случая 
в строгом режиме также будет выводиться ошибка

Чем чревата подобная ошибка:

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

Если использовать строгий режим:

    var run = function(fromWhom){
        "use strict";
        arguments[0] = 'alien';
        alert(fromWhom);
    }
    run('zombie');
    // alert: 'zombie';

Насколько неочевидным является то, что при изменении аргументов 
(`arguments[0] = 'alien'`) изменяется именованный аргумент `fromWhom`? 
Директива `"use strict"` спасёт вас из этого затруднительного положения.

<blockquote class="twitter-tweet" lang="en"><p>Как короткая строка в JavaScript может сэкономить вам пару часов <a href="http://t.co/frkaShxtTW">http://t.co/frkaShxtTW</a> <a href="https://twitter.com/search?q=%23JavaScript&amp;src=hash">#JavaScript</a> <a href="https://twitter.com/search?q=%23useStrict&amp;src=hash">#useStrict</a></p>&mdash; Pro JavaScript (@ProJavaScript) <a href="https://twitter.com/ProJavaScript/statuses/431487194750918656">Февраль 6, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

**[WoollyMittens][3], пользователь reddit** в [комментариях][4] предложил:

>Вместе с этим можно установить "linter", что бы избежать глупых ошибок даже не запуская код: http://www.jshint.com/ 
Для большинства редакторов есть соответствующий плагин. Можете считать это теми красными волнистыми линиями, которыми подчеркиваются ваши грамматические ошибки, 
когда вы пишете email, но применительно к коду.

Скоро я поясню как можно это все автоматизировать с помощью grunt.
**[loz220][5], пользователь reddit** в [комментариях][6] предложил:

>Неплохой обзор. Посмотреть [полный список того, что делает "use strict", можно здесь][7].

## Материалы для дальнейшего изучения

* [Углубленное исследование классов, наследования и примесей в Javascript.][1]
* [Глубокое использование использования React.js в чистом JavaScript для начинающих (библиотека Facebook)][2]



[1]:http://www.webdesignporto.com/javascript-classes-and-inheritance/?utm_source=internal-further-reading&utm_medium=link&utm_campaign=internal
[2]:http://www.webdesignporto.com/react-js-in-pure-javascript-facebook-library/?utm_source=internal-further-reading&utm_medium=link&utm_campaign=internal
[3]:http://www.reddit.com/user/WoollyMittens
[4]:http://www.reddit.com/r/javascript/comments/1x728r/how_a_small_string_can_save_you_hours_in/
[5]:http://www.reddit.com/user/loz220
[6]:http://www.reddit.com/r/javascript/comments/1x728r/how_a_small_string_can_save_you_hours_in/
[7]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode