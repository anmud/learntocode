# Global Execution Context

What happens when JavaScript executes(run) my code?

```js
const = num 3;
function multiplyBy2 (inputNumber){
 const result = inputNumber * 2;
 return result;
}
const name = "Will";
```
Actually, it goes line by line and says "do it". It assigns `data` to lables (`variables` or `const`) in the memory. So, it makes the `data` available by the name. 

As soon as we start running our `code`, we create a `global execution context`
- thread of execution (parsing and executing the code line after line)
- live memory of `variables` with `data` (known as `Global Variable Environment`)

### The thread in JavaScript
- single threaded (one thing at a time)
- synchronous execution (one after another, after another ...)(for now)

