# Property Access

Each item in an array has a numbered position. We can access individual items using their numbers, just like we would in an ordinary list.

Something important to note is that JavaScript starts counting from `0` rather than `1`, so the first item in an array will be at position `0`. This is because JavaScript is zero-indexed.

We can select the first item in an array like this:

```js
let newYearsResolutions = ['Rappel into a cave', 'Take a falconry class', 'Learn to juggle'];

console.log(newYearsResolutions[0]);
// Output: 'Rappel into a cave'
You can also access individual characters in a string. For instance, you can write:

let hello = 'Hello World';
console.log(hello[6]);
// Output: W
```

`W` will be the output since it's the character in the 6th position. This works because JavaScript stores strings in a similar way that it stores arrays.
