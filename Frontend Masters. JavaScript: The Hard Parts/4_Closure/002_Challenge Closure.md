# Challenge Closure

**Challenge 1**
Create a function `createFunction` that creates and returns a `function`. When that created `function` is called, it should print "hello".
```js
var function1 = createFunction();
// now we'll call the function we just created
function1(); //should console.log('hello');
```

**Challenge 2**
Create a function `createFunctionPrinter` that accepts one input and returns a `function`. When that created function is called, it should print out the input that was used when the function was created.
```js
var printSample = createFunctionPrinter('sample');
var printHello = createFunctionPrinter('hello')
// now we'll call the functions we just created
printSample(); //should console.log('sample');
printHello(); //should console.log('hello');
```
**Challenge 3**
Examine the code for the `outer` function. Notice that we are returning a function and that function is using variables that are outside of its scope.
Try to deduce the output before executing.

**Challenge 4**
Now we are going to create a function `addByX` that returns a `function` that will add an input by `x`.
```js
var addByTwo = addByX(2);
addByTwo(1); //should return 3
addByTwo(2); //should return 4
addByTwo(3); //should return 5

var addByThree = addByX(3);
addByThree(1); //should return 4
addByThree(2); //should return 5

var addByFour = addByX(4);
addByFour(4); //should return 8
addByFour(10); //should return 14
```

### Solution

```js
//1
function createFunction() {
function sayHello(){
  console.log("Hello!")
}
  return sayHello;
}

var function1 = createFunction();
function1();


//2
function createFunctionPrinter(input) {
 function print(){
   console.log(input);
 }
  return print;
}
var printSample = createFunctionPrinter('sample');
printSample();
var printHello = createFunctionPrinter('hello');
printHello();


//3
function outer() {
  var counter = 0; // this variable is outside incrementCounter's scope
  function incrementCounter () {
    counter ++;
    console.log('counter', counter);
  }
  return incrementCounter;
}

var willCounter = outer();
var jasCounter = outer();

// Uncomment each of these lines one by one.
// Before your do, guess what will be logged from each function call.

willCounter(); //should return 1
willCounter(); //should return 2
willCounter(); //should return 3

jasCounter(); //should return 1
willCounter(); //should return 4


//4
function addByX(x) {
  
  function addInputByX(y){
   return  (y + x); 
 }
  
  return addInputByX;
}

var addByTwo = addByX(2);

// now call addByTwo with an input of 1
addByTwo(1); //should return 3
addByTwo(2); //should return 4
addByTwo(3); //should return 5

var addByThree = addByX(3);
addByThree(1); //should return 4
addByThree(2); //should return 5

var addByFour = addByX(4);
addByFour(4); //should return 8
addByFour(10); //should return 14
```



