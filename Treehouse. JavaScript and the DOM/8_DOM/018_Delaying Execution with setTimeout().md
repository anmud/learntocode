# Delaying Execution with `setTimeout()`

Why to pass one `function` into another `function` can be a useful thing to do? It allows you to have more control over when and how a `function` gets executed. 

Let's say we want to delay the execution of the anonimous `function`.

```js
function exec (func, arg) {
  func(arg);
}

exec((something) => {
  console.log(something);
}, 'Greetings, everyone');
```
We can use for this `.setTimeout` method. [MDN page for setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)

**Syntax**
```js
var timeoutID = scope.setTimeout(function[, delay, param1, param2, ...]);
```
Method expects the `function` to be the first `parameter`, and integer - which represents the `delay`. And after that we can pass in any `arguments` we want a `function` to recieve, when it finally executes. 

It will look like
```js
window.setTimeout((something) => {
  console.log(something);
}, 3000, 'Greetings, everyone'); //3000=3seconds
```


