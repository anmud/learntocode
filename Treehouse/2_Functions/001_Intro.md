# Functions

**The basic structure of a function:**

```js
function myFunction() {
  // do a bunch of stuff here
}
```

**Calling a function:**

```js
myFunction();
```
**A function expression:**

```js
var myFunction =  function () {
  // do stuff here
};
```

Simple - a functions is a bunch of instructions, that you want to run over and over and over again. 

### Function Names

* can only be made of letters, numbers, the _, and $ characters
* they can't start with a number
* they can't include any spaces or other punctuation

In a `function` the JavaScript you place inside the braces - is run whenever a function is activated. To activate the programming inside the function - you "call" the `function`. 

```js 
function goToCoofeeShop() {
  alert ('Espresso is on the way!');
}
```
To activate the programming inside the function - you "call" the `function`. 

```js 
function goToCoofeeShop() {
  alert ('Espresso is on the way!');
}
goToCofeeShop();
```

The `()` are important - these are what call a function and activate its programming

### Example

Let's create a `function` that each time it's called - opens an alert with a new random number in it:
It's common to programmers to put `functions` at the top of the file. **Remember** the code in the `function` doesn't run immediately - it's simply memorised by the browser!

We indented the code inside the `function`. It makes it easier to see that the code belongs to the `function`. 

```js
function alertRandom(){
 var randomNumber = Math.floor( Math.random() * 6 ) + 1;
 alert(randomNumber);
}
```
Now the browser've read the `function` in the memory and it's prepared to act on its instructions  - as soon as we call it:

```js
function alertRandom(){
 var randomNumber = Math.floor( Math.random() * 6 ) + 1;
 alert(randomNumber);
}
alertRandom();
```
To run the `function` agan - just call it

```js
function alertRandom(){
 var randomNumber = Math.floor( Math.random() * 6 ) + 1;
 alert(randomNumber);
}
alertRandom(); //here we call a function first time
alertRandom(); //here we call a function second time
alertRandom(); //here we call a function third time
alertRandom(); //here we call a function forth time 
```

Now imagine you have fifty lines of JavaScript - only one line of code runs all fifty lines of JavaScript. Very efficient!

There is anorther way to create a `function`, called a `function expression`. You assign a `function` to a variable. Another words we store a function into a variable. 

```js
var alertRandom = function(){
var randomNumber = Math.floor( Math.random() * 6 ) + 1;
 alert(randomNumber);
};
```
We can call a `function expression` the same way we call a `name function`


```js
var alertRandom = function(){
var randomNumber = Math.floor( Math.random() * 6 ) + 1;
 alert(randomNumber);
};
alertRandom(); //here we call a function expression
```







