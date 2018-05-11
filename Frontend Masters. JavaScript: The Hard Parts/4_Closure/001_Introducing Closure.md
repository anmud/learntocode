# Introducing Closure 

When our `functions` get called, we create a `live store of data` (local memory/variable environment/state) for that function’s `execution context`. When the `function` finishes executing, its `local memory` is deleted (except the
returned `value`).

But what if our `functions` could hold on to live data/state between executions? !

This would let our `function definitions` have an associated `cache/persistent memory`. **But it starts with returning us returning a function from another function.**

We just saw that `functions` can be returned from other `functions` in JavaScript
```js
function instructionGenerator() {
function multiplyBy2 (num){
return num*2;
}
return multiplyBy2;
}
let generatedFunc = instructionGenerator()
```
How can we run/call `multiplyBy2` now?
Let's call (run) our generated function with the input `3`
```js
function instructionGenerator() {
function multiplyBy2 (num){
return num*2;
}
return multiplyBy2;
}
let generatedFunc = instructionGenerator()
let result = generatedFunc(3) //6
```
