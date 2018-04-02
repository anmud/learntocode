# Create a Variable: let

Constant variables, as their name implies, are constant — you cannot assign them a different value.

Let variables however, can be reassigned.

```js
let meal = 'Enchiladas';
console.log(meal);
meal = 'Tacos';
console.log(meal);
// output: Enchiladas
// output: Tacos
```
In the example above, the `let` keyword is used to create the `meal` variable with the string `'Enchiladas'` saved to it. On line three, the `meal` variable is changed to store the string `'Tacos'`.

You may be wondering, when to use const vs let. In general, only use const if the value saved to a variable does not change in your program.

