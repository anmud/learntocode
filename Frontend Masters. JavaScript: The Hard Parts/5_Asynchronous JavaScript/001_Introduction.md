# Introducing Asynchronous JavaScript

`Asynchronicity` is the backbone of modern web development in JavaScript.  JavaScript is `single threaded` (one command executing at a time) and has a `synchronous execution model` (each line is executed in order the code appears). So what if we need to wait some time before we can execute certain bits of code? We need to wait on fresh data from an API/server request or for a timer to complete and then execute our code.  We have a `conundrum` - a tension between wanting to delay some `code execution`, but not wanting to block the thread from any further code running while we wait.

What do we do? Let’s see two examples. 

In what order will our console logs occur?
```js
function printHello(){
console.log(“Hello”);
}
setTimeout(printHello,1000);
console.log(“Me first!”);
```
No blocking!?

The result will be:

```js 
"Me first" //console.logs it first
"Hello" // console.logs it after "Me first"
```
Our previous model of JavaScript execution is
insufficient.

In what order will our console logs occur?
```js
function printHello(){
console.log(“Hello”);
}
setTimeout(printHello,0);
console.log(“Me first!”);
```
The result will be:

```js 
"Me first" //console.logs it first
"Hello" // console.logs it after "Me first"
```
Our previous model of JavaScript execution is
insufficient.

**We need to introduce 3 new components of our platform:**
- Thread of execution
- Memory/variable environment
- Call stack

**Adding:**
- Web Browser APIs/Node background threads
- Callback/Message queue
- Event loop