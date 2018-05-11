# Higher-Order Functions & Callbacks

1. takes a `function` as an input (`argument`)

```js
element.addEventListener("click", function(){

  console.log("element clicked!");

});
```

2. returns the `function` as the output

```js
var add = function(num){
  var num1 = num;

  return addToNum1 = function(num2){
    return num1 + num2;
  };

};
```

## Callbacks examples

```js
var ifElse = function(condition, isTrue, isFalse){

  if(condition){
    isTrue;
  } else {
    isFalse;
  }
};

ifElse(true,

 function(){ console.log(true);},

 function(){ console.log(false);}

); //undefined cos we are not returning and not calling them 
```
```js
var ifElse = function(condition, isTrue, isFalse){

  if(condition){
    return isTrue();
  } else {
    return isFalse();
  }
};

ifElse(true,

 function(){ console.log(true);},

 function(){ console.log(false);}

); //true 
```
When we call a `function`, that is a `parameter` or that is an `argument` - it's just like referensing it as a `variable`.

We could also pass in orther `variable` names. 

```js
var ifElse = function(condition, isTrue, isFalse){
  if(condition){
    isTrue();
  } else {
    isFalse();
  }
};

var logTrue = function(){ console.log(true); };
var logFalse = function(){ console.log(false); };

ifElse(false,logTrue,logFalse); //false 
```
