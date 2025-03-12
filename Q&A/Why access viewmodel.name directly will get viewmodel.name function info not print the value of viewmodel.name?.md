# Why access viewmodel.name directly will get viewmodel.name function info not print the value of viewmodel.name?
## answer
If we access the property of a view model directly, it will get the function info of property since it is a `getter-setter` method (not `getter-setter` property).

## examples
### wrong examples
#### wrong example 1
For example, 

```
var Person = $.views.viewModels({ // Compile a Person View Model
  getters: ["name","money"]
});

let nico = Person("Nico","3.50");
console.log(nico.name);
nico.name = "Akari";
```

`console.log(nico.name);` will print the function info of `nico.name`, not the value of `nico.name`.

To access the value of `nico.name`, we should use `nico.name()`. 

Additionally, `nico.name = "Akari";` may cause the error, not set the name of nico as `Akari`.

To set the name of nico as `Akari`, we should use `nico.name("Akari");`.

### fixed examples
#### fixed example 1
The above code snippets in wrong example 1 section should be fixed as follows.

```
var Person = $.views.viewModels({ // Compile a Person View Model
  getters: ["name","money"]
});

let nico = Person("Nico","3.50");
console.log(nico.name());
nico.name("Akari");
```

> [!TIP]
> You can know it if you observe the code snippets from [API: $.views.viewModels section in `$.views.viewModels`article (JsRender docs)](https://www.jsviews.com/#viewmodelsapi@compile) carefully.
>
> <img width="610" alt="image" src="https://github.com/user-attachments/assets/01574b0e-2006-4035-9375-a63c48a9f56e" />
>

## chat with Google Gemini
> [!WARNING]
> Never copy and pasted modified code by Google Gemini (since it produce incorrect code that prints unexpected output on the console.)

I ask

```
Why 

\`\`\`
<!DOCTYPE html5>
<!-- To run the current sample code in your own environment, copy this to an html page. -->

<html>
<head>
  <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
  <script src="https://www.jsviews.com/download/jsviews.min.js"></script>
  <script src="https://www.jsviews.com/download/plugins/jsrender-unicode.min.js"></script>
  <link href="https://www.jsviews.com/samples/samples.css" rel="stylesheet" />
</head>
<body>

<script id="myTmpl" type="text/x-jsrender">
</script>

<div id="page"></div>

<script>

function printPrice(book){
  console.log('The book is at '+ book.price +' price.');
}

var Book = $.views.viewModels({   // Compile a Book View Model
  getters: ["title", "price"],    // getters array - signature of constructor
});

var Person = $.views.viewModels({ // Compile a Person View Model
  getters: ["name","money"],      // getters array - signature of constructor
  extend: {                       // extend object - additional methods 
      purchase: function(other) {
        if(this.money <= other.price)
        {
          throw new Error("Transaction failed. Not enoguh money.");
        }

        this.buy(other);
        return;
      },
      buy: function(other){
        this.money -= other.price;
        console.log('Transcation successful. ' + this.name + ' has purchased a book -- ' + other.title);
        this.printMoney();
      },
      printMoney:function(){
        console.log('The person ' + this.name + ' has ' + this.money + ' money now.');
      }
  }
});

let nico = Person("Nico","3.50");

nico.printMoney();

let book1 = Book("學好日語的秘訣", "1.50"); // Construct a Book View Model instance

printPrice(book1);

nico.buy(book1);

book1.price("2.50");               // Modify price

printPrice(book1);

nico.buy(book1);
</script>

</body>
</html>

\`\`\`

print it on the console of webbrowser developement tool?

\`\`\`
The person function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]} has function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]} money now.
index.html:21 The book is at function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]} price.
index.html:42 Transcation successful. function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]} has purchased a book -- function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]}
index.html:46 The person function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]} has NaN money now.
index.html:21 The book is at function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]} price.
index.html:42 Transcation successful. function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]} has purchased a book -- function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]}
index.html:46 The person function(n){return arguments.length?void(x?x(this).setProperty(e,n):this[t]=n):this[t]} has NaN money now.
\`\`\`
```

<img width="349" alt="image" src="https://github.com/user-attachments/assets/929ec022-7283-43e0-a12f-63c0784c2d9b" />

<img width="362" alt="image" src="https://github.com/user-attachments/assets/d520263a-5627-470f-9819-f59cfff3ec03" />

<img width="370" alt="image" src="https://github.com/user-attachments/assets/21897ba1-337f-432f-923f-df8a842d14b3" />

<img width="367" alt="image" src="https://github.com/user-attachments/assets/b1deb7fc-d286-4a6b-910f-8aae3f572f63" />

<img width="361" alt="image" src="https://github.com/user-attachments/assets/e870398c-5bff-49cc-b4b6-a94c0216e945" />

<img width="364" alt="image" src="https://github.com/user-attachments/assets/bf62c6b9-4db5-41d7-8c96-ba97158b1116" />

And the Google Gemini answers

<img width="617" alt="image" src="https://github.com/user-attachments/assets/a2e5632d-45dd-480a-a86e-9a2a42518cf5" />

<img width="595" alt="image" src="https://github.com/user-attachments/assets/50e1fb01-3225-48b4-8874-71379a25b80a" />

<img width="593" alt="image" src="https://github.com/user-attachments/assets/16911b71-cbc5-4056-8dc3-132f7cd28b57" />

<img width="596" alt="image" src="https://github.com/user-attachments/assets/4465b846-2185-48bf-9c66-cb1934822eb1" />

<img width="619" alt="image" src="https://github.com/user-attachments/assets/2e11a5b0-1c69-49c2-94da-fe87bf5ec04d" />

<img width="576" alt="image" src="https://github.com/user-attachments/assets/8c10186f-958d-4bdf-a66f-13a5991796fb" />

<img width="581" alt="image" src="https://github.com/user-attachments/assets/59079004-b705-4c27-97e3-f5fb6891f215" />

<img width="582" alt="image" src="https://github.com/user-attachments/assets/b85d1351-5e82-4301-b6d4-89dd26becf62" />

<img width="568" alt="image" src="https://github.com/user-attachments/assets/f90bb296-ed2a-4a22-aa60-bc1b324b93a3" />

<img width="542" alt="image" src="https://github.com/user-attachments/assets/4438071b-5f9f-4652-a154-6d14ae65f0cc" />

<img width="555" alt="image" src="https://github.com/user-attachments/assets/ac0d012e-11c2-4c6d-9401-0cf786c2cd54" />

<img width="530" alt="image" src="https://github.com/user-attachments/assets/806c416b-402e-4ac6-9eba-8ed6394eb6c7" />

### modified code by Google Gemini

Thanks to Google Gemini generates the whole modifed code, we don't have to modify, we just need to copy and paste the following modified code by Google Gemini.

```
<!DOCTYPE html5>
<html>
<head>
  <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
  <script src="https://www.jsviews.com/download/jsviews.min.js"></script>
  <script src="https://www.jsviews.com/download/plugins/jsrender-unicode.min.js"></script>
  <link href="https://www.jsviews.com/samples/samples.css" rel="stylesheet" />
</head>
<body>

<script id="myTmpl" type="text/x-jsrender">
</script>

<div id="page"></div>

<script>

function printPrice(book){
  console.log('The book is at '+ book.price +' price.');
}

var Book = $.views.viewModels({
  getters: ["title", "price"],
});

var Person = $.views.viewModels({
  getters: ["name","money"],
  extend: {
    purchase: function(other) {
      if(this.money <= other.price)
      {
        throw new Error("Transaction failed. Not enoguh money.");
      }

      this.buy(other);
      return;
    },
    buy: function(other){
      this.money -= other.price;
      console.log('Transcation successful. ' + this.name + ' has purchased a book -- ' + other.title);
      this.printMoney();
    },
    printMoney:function(){
      console.log('The person ' + this.name + ' has ' + this.money + ' money now.');
    }
  }
});

let nico = Person("Nico", 3.50); // money is now a number.

nico.printMoney();

let book1 = Book("學好日語的秘訣", 1.50); // price is now a number.

printPrice(book1);

nico.buy(book1);

book1.price = 2.50; // Modify price

printPrice(book1);

nico.buy(book1);
</script>

</body>
</html>
```

### fixed code
See [fixed example 1 section in this article](https://github.com/40843245/JSRender/blob/main/ViewModel/$.views.viewModels/$.views.viewModels%20method.md#fixed-example-1)
