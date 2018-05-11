# Callbacks vs. High Order Functions

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

- The `function` we pass in is a `callback function`
- The `outer function` that takes in the `function` (our callback) is a `higher-order function`

### Higher-order functions

Takes in a `function` or passes out a `function`. Just a term to describe these `functions` - any `function` that does it we call that - but there's nothing different about them inherently. 

So  callbacks  and  higher order functions  simplify our code and keep it DRY. And they do something even more powerful.
They allow us to run `asynchronous` code.



