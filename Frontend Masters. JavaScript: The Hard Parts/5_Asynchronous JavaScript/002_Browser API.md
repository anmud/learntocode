# Browser API

**Let’s see the first of these (the Web Browser API) in action**

```js
function printHello(){
console.log(“Hello”);
}
setTimeout(printHello,0); 
console.log(“Me first!”); //console.logs ""
```
### Step-by-step

1. declares `printHello` function in the global memory 
2. the next line says: 'execute Timeout' (we call it ), and we pass it our `printHello` function and value of `0`
3. `Timeout` feature lives in the `Web Browser API`. When we call our `setTimeout` function - behind the scenes it's making communication with the web browser
4. so our `setTimeout` function speaks to the `Web Browser API`, it speaks to `timer` feature
5. timer has a reference to `printHello` function
6. it checks if `timer` is complete or not
7. console.logs "Me first"
8. now our `timer` completes in the background
9. then `printHello` function is pushed in the `call stack`
10. `printHello` function is executed in its lockal execution context and prints "Hello"


