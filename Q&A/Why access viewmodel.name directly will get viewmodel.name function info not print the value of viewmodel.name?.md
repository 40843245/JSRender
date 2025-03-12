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
