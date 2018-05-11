# Local Execution Context

### Running/calling/invoking a function

This is not the same as defining a `function`
```js
const num = 3;
function multiplyBy2 (inputNumber){
const result = inputNumber*2;
return result;
}
const output = multiplyBy2(4);
const newOutput = multiplyBy2(10);
```
When you execute a `function` you create a new `execution context` comprising:

1. The thread of execution (we go through the `code` in the `function` line by line)
2. A local memory (`Variable environment`) where anything defined in the `function` is stored