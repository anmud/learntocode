# Properties

When you introduce a new piece of data into a JavaScript program, the browser saves it as an instance of the data type. An instance is an individual case (or object) of a data type.

JavaScript will save a new piece of data, like `'Hello'`, as a string instance in the computer's memory. Another example, the number `40.7`, is stored as an instance of the number data type.

An instance, like the string `'Hello'`, has additional information attached to it.

For example, every string instance has a property called `length` that stores the number of characters in it. You can retrieve property information by appending the string with a period and the property name:

```js
console.log('Hello'.length);
```

In the example above, the value saved to the `length` property is retrieved from the string, `'Hello'`. The program prints 5 to the console, because Hello has five characters in it.