# Passing Arguments

### Example 1

```js
var increment = function(n){ return n + 1; };

var square = function(n){ return n*n; };

var doMathSoIDontHaveTo = function(n, func){ return func(n); };

doMathSoIDontHaveTo(5, square); //25

doMathSoIDontHaveTo(4, increment); //5 
```
### Example 2

How to pass an additional `argument` 

```js
var ifElse = function(condition, isTrue, isFalse, arg){ //first add a peremeter
  if(condition){
    isTrue(arg); //add argument 
  } else {
    isFalse(arg);
  }
};

ifElse(true, function.., function.., 5); //call a function with arguments
```