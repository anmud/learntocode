# Callback Queue

Now we are interacting with a world outside of JavaScript. We need a way of predictably understanding how this outside world will interact with our JavaScript execution model. What would happen here?

```js
function printHello(){
console.log(“Hello”);
}
function blockFor1Sec(){
//blocks in the JavaScript thread for 1 second
}
setTimeout(printHello,0);
blockFor1Sec()
console.log(“Me first!”);
```

We have two rules for the execution of our asynchronously delayed code
1. Hold each deferred `function` in a queue (the `Callback Queue`) when the API ‘completes’
2. Add the `function` to the `Call stack` (i.e. execute the
`function`) ONLY when the `call stack` is totally empty (Have the Event Loop check this condition)

