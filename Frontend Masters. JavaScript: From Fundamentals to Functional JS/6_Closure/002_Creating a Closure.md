# Creating a Closure

```js
var closureAlert = function(){ 
  var x = 0; 
  var alerter = function(){ 
    alert(++x); 
  }; 
  return alerter; 
}; 

var funcStorer = closureAlert(); 
var funcStorer2 = closureAlert(); 
funcStorer(); //alerts 1
funcStorer(); //alerts 2
funcStorer2(); //alerts 1 (every time we call we have a new scope)
```
We return `alerter` which means that when we call `closureAlert`, we enter into the `function` body. First that it does it initialises `x` to `0`, ut sees that we have `alerter` function, skips over ot and then returns it. So our `funcStorer` is storing `alerter`. If want to call `alerter`, we should call `funcStorer()`. 
