# Arguments Keyword
`Arguments` keyword is a special keyword in JS that lives inside `functions` and gets the `value` of the `arguments` you pass in, and in a form like - `an-array-like object`. 

```js
var add = function(a, b){
    console.log(arguments); //logs [3,10,5]
 	return a + b; 
};
add(3, 10, 5); //13
```
If we want to return `18` as a result

```js
var add = function(a, b){
    console.log(arguments); //logs [3,10,5]
 	return a + b + arguments[2]; //add the index of arguments 'array'
};
add(3, 10, 5); //18
```
**NOTE** `arguments keyword` is not reall `array` - it's `an array-like object`. It's important for when you are trying to use array `methods` on it. 
```js
var add = function(a, b){
  arguments.slice(0,1) //ERROR!!  
  return a + b; 
};
add(3, 10, 5);
```
If you want to use array `methods` you have to first turn it to a reall `array`. 
```js
var add = function(a, b){
  array.prototype.slice.call(arguments, 0 ) 
  return a + b; 
};
add(3, 10, 5);
```