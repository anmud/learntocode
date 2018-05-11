# Challenge

**Challenge 1** 

Create a function `addTwo` that accepts one `input` and adds `2` to it.

**Challenge 2**

Create a function `addS` that accepts one input and adds an `s` to it.

**Challenge 3**

Create a function called `map` that takes two inputs: an `array` of numbers (a list of numbers); a `callback` function - a `function` that is applied to each `element` of the `array` (inside of the function `map`). Have `map` return a new `array` filled with `numbers` that are the result of using the `callback` function on each element of the input array.

  
**Challenge 4** 

The function `forEach` takes an `array` and a `callback`, and runs the `callback` on `each element` of the `array`. `forEach` does not return anything.

**Extension 1**

In the first part of the extension, you're going to rebuild `map` as `mapWith`. This time you're going to use `forEach` inside of `mapWith` instead of using a `for` loop.

**Extension 2**

The function `reduce` takes an `array` and reduces the elements to a single `value.` For example it can sum all the numbers, multiply them, or any operation that you can put into a function.

Here's how it works. The `function` has an `accumulator value` which starts as the `initialValue` and accumulates the output of `each` loop. The `array` is iterated over, passing the `accumulator` and the `next array element` as `arguments` to the `callback`. The `callback's return value` becomes the new `accumulator` value. The next `loop` executes with this new `accumulator value`. In the example above, the accumulator begins at `0`. `add(0,4)` is called. The `accumulator's value` is now `4`. Then `add(4, 1)` to make it `5`. Finally `add(5, 3)` brings it to `8`, which is returned.

### Solutions

```js

// Challenge 1
function addTwo(num) {
 const result = num + 2;
  return result;
}

console.log(addTwo(3));
console.log(addTwo(10));


// Challenge 2
function addS(word) {
const newWord = word + 's';
  return newWord;
}

console.log(addS('pizza'));
console.log(addS('bagel'));


// Challenge 3
function map(array, callback) {
	let output = [];
	for(let i = 0; i < array.length; i++) {
		output.push(callback(array[i]));
	}
	return output;
}
 
console.log(map([1, 2, 3], addTwo));


// Challenge 4
function forEach(array, callback) {
for(let i = 0; i < array.length; i++) {
		callback(array[i]);
}
}

var alphabet = '';
var letters = ['a', 'b', 'c', 'd'];

forEach(letters, function(char) {
  alphabet += char;
});

console.log(alphabet); 

//--------------------------------------------------
// Extension
//--------------------------------------------------

//Extension 1
function mapWith(array, callback) {
let output = [];
array.forEach(function(arrayElement){
  output.push(callback(arrayElement))
 })
return output;
};


console.log(map([1, 2, 3], addTwo));
  
//Extension 2
function reduce(array, callback, initialValue) {
	let accumulator = initialValue;
	array.forEach(function(element) {
		accumulator = callback(accumulator, element);
	});
	return accumulator;
}

var nums = [4, 1, 3];
var add = function(a, b) { return a + b; }
console.log(reduce(nums, add, 0));   //-> 8
```

