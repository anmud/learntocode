# Challenge Callbacks

1. Write a `function`, `funcCaller`, that takes a `func` (a function) and an `arg` (any data type). The function returns the `func` called with `arg`(as an argument).

2. Write a `function`, `firstVal`, that takes an `array`, `arr`, and a `function`, `func`, and calls `func` with the first `index of the arr`, the `index #` and the whole `array`.

3. Change `firstVal` to work not only with `arrays` but also `objects`. Since `objects` are not ordered, you can use any `key-value pair` on the `object`.

### Solution
```js
//1
var functionCaller = function(func, arg){
    return func(arg);
}

//2 
var firstVal = function(arr, func){
func(arr[0], 0, arr);
}

//3
var firstVal = function(list, func){
    if( arr.isArray(list) ){
     return func(arr[0], 0, arr);
    } else {
     for(var k in list){
         return func(list[k], k, list);
     }
    }
}
```
