# Choose the Right Iterator

1. To use a method that will do something to each of the values in the array and return undefined, we choose: `.forEach`

2. To use a method that will return a new array with only those elements longer than 7 characters, we choose: `.filter`

3. To use a method that will return a new array of numbers returned from the function, we choose: `.map`

4. To use a method that will return a boolean value, we choose: `.some`

![choose-a-method](../choose-a-method.png)

## Let's review!

1. `.forEach()` is used to execute the same code on every element in an array but does not change the array and returns undefined.
2. `.map()` executes the same code on every element in an array and returns a new array with the updated elements.
3. `.filter()` checks every element in an array to see if it meets certain criteria and returns a new array with the elements that return truthy for the criteria.
4. All iterator methods can be written using arrow function syntax. In fact, given the succinctness and the implicit return of arrow function syntax, this is quickly becoming the preferred way to write these types of method calls.
5. You can visit the Mozilla Developer Network to learn more about iterator methods (and all other parts of JavaScript!).
6. Additional iterator methods such as `.some()`, `.every()`, `.reduce()` perform different functions.

