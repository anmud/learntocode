# Arrow functions

What is an `arrow function`? 

1.  No need for `return statement`. `return` is implied if using an `expression` after an `arrow`.

```js
const triple = num => num * 3
  // if only one argument not parens, if more you need parens
```

2. Parens are optional depending on the number of arguments

```js
let square = x => x * x;
console.log(square(10)) // 100

let add2 = (a,b) => a + b;
console.log(add2(3,4)); // 7 
```
3. If we use `curly braces` (`{}`) in an `arrow function` we need always to define a `return statement` 
```js
var triple = function triple(num) {
  return num * 3;
}; // inside of {} parens is a scope of a functions. 
```

3. We use `curly braces` if we need a `statement`, not `expression`
```js
var add = function add(num1, num2) {
  return num1 + num2;
}; 
```

What is the difference between `expression` and `statement`?

`expressions` = a code that evaluates to a value e.g `num1 + num2 = 5`
`statement` = computer has to do something e.g. `if then else`, `return`

```js
var arrowUserIsAdmin = function arrowUserIsAdmin(user) {
  if (user.isAdmin) {
    return "true";
  } else return "false";
};

console.log(arrowUserIsAdmin(user));
// result - "false"
```