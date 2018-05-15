# Challenge

### **Challenge 1**
- Write code that will log to the console, 'I am at the beginning of the code'.

- Beneath that `console log`, set a `timer` (see setTimeout) that will log to the console `I am in the setTimeout callback function` after `3` seconds (3000 ms)

- Next, add code to the end of the challenge to log `I am at the end of the code`. Now re-run the code.

- Make sure the `console` and `output` panes are showing (click the tabs above if not) and then run your code with the `Run with JS` button.

- Clear the `console`. Change the delay time in the time from `3000` ms to `0`. Think hard about how the order should change and then run the code again.

**Solution**

```js
function print(){
  console.log("I am in the setTimeout callback function")
}
setTimeout(print, 3000)
console.log("I am at the beginning of the code")

console.log('End of Challenge 1');

console.log("I am at the end of the code")
```

### **Challenge 2**
1. Write code that will log to the console `Interval Hello!` every `2` seconds (see setInterval). Use the given `clearAllIntervals` function to clear all the messages when you have this functionality working.

2. Next, modify your code so that the `Interval Hello!` messages will automatically stop after `10` seconds.

3. Then, modify your code again so that the `Interval Hello!` messages will automatically stop after `10` seconds without use of the `clearAllIntervals` function, and using `clearInterval` only once. Perform research if you are unsure how to do this.

**Solution**

1. 
```js
function print(){
  console.log("Interval hello")
}

setInterval(function(){print()}, 2000)

function clearAllIntervals() {
  for (let i = 0; i < 1000; i++) {
    clearInterval(i);
  }
}
clearAllIntervals();
```
2. 
---
3. 
```js
function print(){
  console.log("Interval hello")
}

var ID = setInterval(function(){print()}, 2000)

setTimeout(function(){clearInterval(ID);}, 10000)
```
