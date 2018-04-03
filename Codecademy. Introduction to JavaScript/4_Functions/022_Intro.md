# Introduction to Functions

A function is a block of code designed to perform a task.

Functions are like recipes. They accept data, perform actions on that data, and return a result. The beauty of functions is that they allow us to write a block of code once, then we can reuse it over and over without rewriting the same code.

Take a look at the code in this exercise. This code turns the calculator on if it is currently off, and turns it off if the calculator is currently on.

See if you can figure out how this code works. In the next exercise, we'll walk through it line by line.

![functions-intro](../functions-intro.png)

## How does this code work?

```js
let calculatorIsOn = false;

const pressPowerButton = () => {
  if (calculatorIsOn) {
    console.log('Calculator turning off.');
    calculatorIsOn = false;
  } else {
    console.log('Calculator turning on.');
    calculatorIsOn = true;
  }
};

pressPowerButton();
// Output: Calculator turning on.

pressPowerButton();
// Output: Calculator turning off.
```

Let's explore each part in detail.

1. We created a function named `pressPowerButton`.

`const pressPowerButton` creates a variable with a given name written in camelCase.

The variable is then set equal `=` to a set of parentheses followed by an arrow token `() =>`, indicating the variable stores a function. This syntax is known as arrow function syntax.

Finally, between the curly braces `{}` is the function body, or the JavaScript statements that define the function. This is followed by a semi-colon `;`. In JavaScript, any code between curly braces is also known as a block.

2. Inside the function body is an `if`/`else` statement. 

3. On the last few lines, we call the function by writing its name followed by a semi-colon `pressPowerButton();`. This executes the function, running all code within the function body. 

4. We executed the code in the function body twice without having to write the same set of instructions twice. Functions can make code reusable!

### Example 2

![functions-example](../functions-example.png)

