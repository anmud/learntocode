# Arrow Functions

JavaScript also provides several ways to refactor arrow function syntax. We'll explore a few of these techniques here, using an example function from a previous exercise.

```js
const multiplyByNineFifths = (celsius) => {
  return celsius * (9/5);
};

const getFahrenheit = (celsius) => {
  return multiplyByNineFifths(celsius) + 32;
};

console.log('The temperature is ' + getFahrenheit(15) + '°F');
```
We can refactor this function in three ways. The most condensed form of the function is known as *concise body*.

1. Functions that take a single parameter should not use parentheses. The code will still work, but it's better practice to omit the parentheses around single parameters. However, if a function takes zero or multiple parameters, parentheses are required.
2. A function composed of a sole single-line block is automatically returned. The contents of the block should immediately follow the arrow `=>` and the `return` keyword can be removed. This is referred to as implicit return.
3. A function composed of a sole single-line block does not need brackets.
In other words, the previous code can be refactored like this:

```js
const multiplyByNineFifths = celsius => celsius * (9/5);

const getFahrenheit = celsius => multiplyByNineFifths(celsius) + 32;

console.log('The temperature is ' + getFahrenheit(15) + '°F');
```
You'll notice:

1. The parentheses around `celsius` have been removed, since it is a single parameter.
2. The `return` keyword has been removed since the function consists of a single-line block.
3. The `{}` have been removed, again, since the function consists of a single-line block.