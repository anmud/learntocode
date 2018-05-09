# Closures & Functional Programming

Here is an example of how we can use closure. So, maybe we have `add` function and want a generic `call`. 

```js
var add = function(num){
  var num1 = num;

  var addToNum1 = function(num2){
    return num1 + num2;
  };

  return addToNum1;
};
var add5 = add(5);
```

And now we have `add5` function that we can call later with another number. 

```js
var add = function(num){
  var num1 = num;

  var addToNum1 = function(num2){
    return num1 + num2;
  };

  return addToNum1;
};
var add5 = add(5);
add5(2); // 7
```

### Step-by-step how this is working

* We remember the `function` and skip down to the bottom. 
* we call `add` function and assign it to the variable `add5`
* we go into the `function body` and pass the `argument` to the `function`
* `num` is now `5`
* we create a local variable `num1` wchich takes the `argument`
* we see the new `function` and skip it, then return this `function` 
* we are calling the `add5` function with the argument `2`
* we go back up to `addToNum1` function which already has `num1` and pass argument `2`, so now `num2` = `2`
* we get `7` as a result
