# Built-in Methods

While the length of a string is calculated when an instance is created, a string instance also has methods that calculate new information as needed. When these built-in methods are called on an instance, they perform actions that generate an output.

Built-in methods are called, or used, by appending an instance with a period, the name of the method, and opening (`(`) and closing (`)`) parentheses. Consider the examples below:

```js
console.log('Hello'.toUpperCase()); // 'HELLO'
console.log('Hey'.startsWith('H')); // true
```
Let's look at each line separately:

On the first line, the `.toUpperCase()` method is called on the string instance `'Hello'`. The result is logged to the console. This method returns a string in all capital letters: `'HELLO'`.

On the second line, the `.startsWith()` method is called on the string instance `"Hey"`. This method also accepts the character `'H'` as an input between the opening and closing parentheses. Since the string `'Hey'` does start with the letter `'H'`, the method returns the boolean true.

You can find a list of built-in string methods in the [JavaScript documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/prototype). Developers use documentation as a reference tool. It describes JavaScript's keywords, methods, and syntax.