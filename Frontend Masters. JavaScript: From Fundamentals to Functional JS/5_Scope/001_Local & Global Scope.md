# Local & Global Scope

`Scope` is created dinamically whenever we call a `function`. So, every time we call a `function`, we create a new `scope`. And that's why we can have different `values` in a `function` body, using the same `function`.

`Local Scope` - this is how we create a scope in JS is by wrapping it in a `function`.  

```js
var func = function(){
  var local = true;
};

console.log(local); //this is outside of the scope and it will give us an error, cos there is no global variable there
```

`Global Scope` - global `variables` can be accessed anywhere in your application 

```js
var x = 'global!';

//inside a function
function encapsulate(){

z = 'global here, too!';

}
```

You also can put it in a `window object` - so all global variales are located in a window object. 

```js
var x = 'global!';
//inside a function
function encapsulate(){
  z = 'global here, too!';

  window.y = 'also global!';
}
```
