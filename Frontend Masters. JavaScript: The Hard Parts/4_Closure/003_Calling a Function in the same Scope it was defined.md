# Calling a Function in the same Scope as it was defined

```js
function outer (){
let counter = 0;
function incrementCounter (){
counter ++;
}
incrementCounter();
}
outer();
```
Where you define your `functions` determines what `variables` your `function` have access to when you call the `function`.

But what if we call our `function` outside of where it was defined?

```js
function outer (){
let counter = 0;
function incrementCounter (){
counter ++;
}
}
outer()
incrementCounter();
```
What happens here?

There is a way to run a `function` outside where it was defined - return the `function` and assign it to a new `variable`.

```js
function outer (){
let counter = 0;
function incrementCounter (){
counter ++;
}
return incrementCounter;
}
var myNewFunction = outer(); // myNewFunction = incrementCounter
myNewFunction(); //1
myNewFunction(); //2
```

