# Parametising Functions

To generalise a `function` we can add a `parameter` - we can parametise our `function`. 

Now suppose we have a function copyArrayAndMultiplyBy2. Let's diagram it out

```js
function copyArrayAndMultiplyBy2(array) {
let output = [];
for (let i = 0; i < array.length; i++) {
output.push(array[i] * 2);
}
return output;
}
const myArray = [1,2,3]
let result = copyArrayAndMultiplyBy2(myArray)
```

What if want to copy array and divide by 2?

```js
function copyArrayAndDivideBy2(array) {
let output = [];
for (let i = 0; i < array.length; i++) {
output.push(array[i] /2);
}
return output;
}
const myArray = [1,2,3]
let result = copyArrayAndDivideBy2(myArray);
```

We could generalize our function so that we pass in our specific instruction only when we run the `copyArrayAndManipulate` function!

```js
function copyArrayAndManipulate(array, instructions) {
let output = [];
for (let i = 0; i < array.length; i++) {
output.push(instructions(array[i]));
}
return output;
}
function multiplyBy2(input) {
return input * 2;
}
let result = copyArrayAndManipulate([1, 2, 3], multiplyBy2);
```
