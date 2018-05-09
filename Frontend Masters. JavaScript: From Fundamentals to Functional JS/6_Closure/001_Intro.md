# Closure Intro

A `closure` happens when you return a `function` from inside of a `function`, and that inner `function` retains access to the `scope`.

### Example 1

```js
var closureAlert = function(){
  var x = "Help! I'm a variable stuck in a closure!";
  var alerter = function(){
    alert(x);
  };
  alerter();
};

closureAlert();
```
### Example 2

```js
var closureAlert = function(){
  var x = "Help! I'm a variable stuck in a closure!";

  var alerter = function(){
    alert(x);
  };

  setTimeout(alerter, 1000);

  console.log('will still run right after');
};
closureAlert();
//in one second...
```
### Step-by-step

1. defining a `closureAlert` function and then remember it and skip it. 
2. call `closureAlert` function and go inside of its body, it assigns `string` to `x` variable. 
3. then it remembers the `alerter` functions and skips it
4. it sets the `timeout` to wait a second after we call a `function`
5. `console.log`'s a string
6. calls `closureAlert` and runs it's body
7. runs `alerter` function in a second 