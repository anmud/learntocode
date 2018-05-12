# Lexical Scope

When a `function` is defined, it gets a `[[scope]] property` that references the `Local Memory/Variable Environment` in which it has been defined.

```js
function outer (){
let counter = 0;
function incrementCounter (){
counter ++;
}
return incrementCounter;
}
let myNewFunction = outer(); // myNewFunction = incrementCounter
myNewFunction();
myNewFunction();
```
Wherever we call that `incrementCounter` function - it will always look first in its immediate `local memory` (variable environment), and then in the [[scope]] property next before it looks any further up. 

**JavaScript static/lexical scoping** 

This is what it means when we say JavaScript is lexically or statically scoped. Our `lexical` scope (the available live data when our `function` was defined) is what determines our available `variables` and prioritization at `function` execution, not where our `function` is called. 

What if we run 'outer' again and store the returned `incrementCounter` in `anotherFunction`
```js
function outer (){
let counter = 0;
function incrementCounter (){
counter ++;
}
return incrementCounter;
}
let myNewFunction = outer();
myNewFunction(); //1
myNewFunction(); //2
var anotherFunction = outer(); // myNewFunction = incrementCounter
anotherFunction(); //1
anotherFunction(); //2
```
If we declare a `counter` in the `global invironment` the result will be 

```js
function outer (){
function incrementCounter (){
counter ++;
}
return incrementCounter;
}

let counter = 0;
let myNewFunction = outer();
myNewFunction(); //1
myNewFunction(); //2
var anotherFunction = outer(); // myNewFunction = incrementCounter
anotherFunction(); //3
anotherFunction(); //4
```
If we declare a `counter` inside the `incrementCounter` function, the result will be 
```js
function outer (){
function incrementCounter (){
let counter = 0;
counter ++;
}
return incrementCounter;
}

let myNewFunction = outer();
myNewFunction(); //1
myNewFunction(); //1
var anotherFunction = outer(); // myNewFunction = incrementCounter
anotherFunction(); //1
anotherFunction(); //1
```
