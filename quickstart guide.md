# quickstart guide
## install JsRender module
You can install JsRender module with npm command in command-line prompt.

```
npm install jsrender
```

## install JsViews module
Similarly, you can install JsViews module with npm command in command-line prompt.

```
npm install jsviews
```

## load JsRender module
There are three options to load JsRender in the browser as a webpack module (with `require` function call).

+ Load jQuery globally (as a script tag – so `window.jQuery` is defined), then load JsRender as a module in the webpack client script bundle:

    require('jsrender'); // Load JsRender as jQuery plugin (attached to global jQuery)

+ Load both jQuery and JsRender as modules in the webpack client script bundle:
    
    var $ = require('jquery'); // Load jQuery as a module
    require('jsrender')($);    // Load JsRender as jQuery plugin (jQuery instance as parameter)
        

+ Load JsRender as a module in the webpack client script bundle, without loading jQuery at all:
    
    var jsrender = require('jsrender')(); // Load JsRender without jQuery (function call, no parameter)
        
  
> [!NOTE]
> If jQuery is not defined globally, `require('jsrender')` returns a **_function_**.
>
> Calling that function without a parameter then loads JsRender without jQuery (and returns the JsRender namespace).
>
> Alternatively, calling that function with a reference to a jQuery instance as parameter loads JsRender as a plugin (attached to that jQuery instance) – and returns the jQuery instance.

### examples
#### [example 1 – jQuery loaded globally](https://www.jsviews.com/#node/webpack@jquery-global)

**index.html:**

    <html><head>
      <script src=".../jquery...js"></script> <!-- Load jQuery as global -->
    </head><body>
      <div id="container"></div>
      <script src="bundle.js"></script>
    </body></html>
    

**source.js:**

    require('jsrender'); // Load JsRender (jQuery is loaded as global)
    var tmpl = $.templates('Name: {{:name}}');
    var data = {name: 'Jo'};
    var html = tmpl.render(data);
    $('#container').html(html);
    

**command line:**

    webpack ./source.js bundle.js
    

#### [example 1 – jQuery loaded as module](https://www.jsviews.com/#node/webpack@jquery-module)

**index.html:**

    <html><body>
      <div id="container"></div>
      <script src="bundle.js"></script>
    </body></html>
    

**source.js:**

    var $ = require('jquery'); // Load jQuery as a module
    require('jsrender')($);    // Load JsRender as jQuery plugin (jQuery instance as parameter)
    var tmpl = $.templates('Name: {{:name}}');
    var data = {name: 'Jo'};
    var html = tmpl.render(data);
    $('#container').html(html);
    

**command line:**

    webpack ./source.js bundle.js
    

#### [example 1 – JsRender without jQuery](https://www.jsviews.com/#node/webpack@no-jquery)

**index.html:**

    <html><body>
      <div id="container"></div>
      <script src="bundle.js"></script>
    </body></html>
    

**source.js:**

    var jsrender = require('jsrender')(); // Load JsRender without jQuery
    var tmpl = jsrender.templates('Name: {{:name}}');
    var data = {name: 'Jo'};
    var html = tmpl.render(data);
    document.querySelector('#container').innerHTML = html;
    

**command line:**

    webpack ./source.js bundle.js
