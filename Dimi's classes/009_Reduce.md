# Reduce examples of using

**Reduce** is called on every `item` in the `list`, but the end result can be whatever you need; an `array of data`, an `object`, a `number`.
**Reduce** is a way of getting a single `result` from a series of `values`.

1. A basic reduction. 

**Use it when:** You have an `array` of numbers and you want to sum them  up.

```js
const euros = [29.76, 41.85, 46.5]

const sum = euros.reduce((acc, currentEuro) => acc + currentEuro)

console.log(sum) // 118.11
```

**How to use it:**

- In this example, `Reduce` accepts two `parameters`, the *accumulator* and the *current euro*.
- The `reduce method` cycles through each `number` in the `array` 
- When the `loop` starts the *accumulator value* is the `number` on the far left (29.76) and the *current euro* is the one next to it (41.85).
- In this particular example, we want to add the *current euro* to the *accumulator*.
- The calculation is repeated for each `number` in the `array`, but each time the *current euro* changes to the next number in the `array`, moving right.
- When there are no more `numbers` left in the `array` the method returns the *accumulator value*.

2. Finding an Average with the `Reduce Method` In JavaScript​. Instead of logging the `sum`, you could divide the `sum` by the `length of the array` before you return a final value.

The way to do this is by taking advantage of the other `arguments` in the `reduce method`. The first of those `arguments` is the `index`. Much like a `for-loop`, the `index` refers to the `number of times` the `reducer` has looped over the `array`. The last `argument` is the `array` itself.

```js
const euros = [29.76, 41.85, 46.5]

const average = euros.reduce((acc, currentEuro, index, array) => {
 acc += currentEuro
 if(index === array.length - 1){
   return acc / array.length
 } else return acc
})

console.log(average) // 39.37
```

3. `Map` and `Filter` as `Reductions`. The benefit of using `reduce` comes into play when you want to `map` and `filter` together and you have a lot of `data` to go over.


The thing is, you don’t always have to return a `single value`. You can `reduce` an `array` into a `new array`.

For instance, lets reduce an `array` of numbers into another `array` where every `number` is doubled. To do this we need to set the `initial value` for our `accumulator` to an `empty array`. Actually, this operation is the `map` method rewritten as a `reduce method`.

By setting the `initial value` to an `empty array` we can then push each `number` into the `accumulator` (which is an empty array). If we want to `reduce` an `array of values` into another `array` where every `value` is doubled, we need to push the  `number * 2`. Then we return the `accumulator` when there are no more numbers to push.

```js
const euros = [29.76, 41.85, 46.5]

const doubled = euros.reduce((acc, currentEuro) => {
   acc.push(currentEuro * 2)
   return acc
}, [])


console.log(doubled) // [59.52, 83.7, 93]
```

4. We could also `filter` out `numbers` we don’t want to double by adding an `if statement` inside our `reducer`.

```js
const euros = [29.76, 41.85, 46.5]

const above30 = euros.reduce((acc, currentEuro) => {

if(currentEuro > 30){
  acc.push(currentEuro)
}
 return acc
}, [])

console.log(above30) //[41.85, 46.5]
```

5. Count the element frequency with `Reduce Method` In JavaScript​.

**Use it when:** You have a `collection of items` and you want to know how many of each `item` are in the `collection`.

```js
const fruitBasket = ['banana', 'cherry', 'orange', 'apple', 'cherry', 'orange', 'apple', 'banana', 'cherry', 'orange', 'fig' ];

const count = fruitBasket.reduce((acc, fruit) => {

  acc[fruit] = (acc[fruit] || 0) + 1
  return acc

}, {})

console.log(count) // {banana: 2, cherry: 3, orange: 3, apple: 2, fig: 1}
```

To count the frequency of the `items` in an `array` our `initial value` must be an `empty object`, not an `empty array` like it was in the last example.
Since we are going to be returning an `object` we can now store key-value pairs in the `accumulator`.

1) On our first pass, we want the name of the `first key` to be our `current value` and we want to give it a `value` of `1`.
This gives us an `object` with all the `fruit` as `keys`, each with a `value of 1`. 

```js
fruitBasket.reduce( (acc, fruit) => {
  acc[fruit] = 1;
  return acc;
}, {})

console.log() // {banana: 1, cherry: 1, orange: 1, apple: 1, fig: 1}
```
2) Now we want the `amount` of each `fruit` to increase if they repeat. To do this, on our `second loop` we check if our `accumulator` contains a `key` with the `current fruit` of the `reducer`. If it doesn’t then we create it. If it does then we increment the `amount` by one.

```js
fruitBasket.reduce((acc, fruit) => {
  if (!acc[fruit]) {
    acc[fruit] = 1;
  } else {
    acc[fruit] = acc[fruit] + 1;
  }
  return tally;
}, {});
```

At the beginning of the example it was just written in a short form. 

6. Combining an `array of arrays` in a single `array` with the `Reduce Method` In JavaScript​​

We set the `initial value` to an `empty array` and then concatenate the `current value` to the `accumulator` (initial value).

```js
const data = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];

const flat = data.reduce((acc, currentValue) => {

  return acc.concat(currentValue)

}, [])

console.log(flat) // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
**TO REMEMBER:** The `concat()` method is used to merge two or more `arrays`. This method does not change the `existing arrays`, but instead returns a `new array`.

6.1. Lets say we just want all the colors in the `data variable` below.
We’re going to step through each `object` and pull out the `colours`. We do this by pointing `amount.c` for `each object` in the `array`. We then use a `forEach loop` to push every `value` in the `nested array` into our `accumulator`.

```js
const data2 = [
  {a: 'happy', b: 'robin', c: ['blue','green']}, 
  {a: 'tired', b: 'panther', c: ['green','black','orange','blue']}, 
  {a: 'sad', b: 'goldfish', c: ['green','red']}
];

const colors = data2.reduce((acc, currentValue) =>{

  currentValue.c.forEach(color => {
     acc.push(color)
  })
    return acc
}, [])

console.log(colors) // ["blue", "green", "green", "black", "orange", "blue", "green", "red"]
```
**TO REMEMBER:** The `forEach()` method calls a provided `function` once for `each element` in an `array`, in order.


If we only need `unique number` then we can check to see of the `number` already exists in `accumulator` before we push it.

```js
const uniqueColors = data2.reduce((acc, currentValue) =>{
 
  currentValue.c.forEach( color => {
  if(acc.indexOf(color) === -1){
     acc.push(color)
  }
  });
   return acc
}, [])

console.log(uniqueColors) // ["blue", "green", "black", "orange", "red"]
```

**TO REMEMBER:** The `indexOf()` method searches the `array` for the specified `item`, and returns its position. The search will start at the specified position, or at the beginning if no start position is specified, and end the search at the end of the `array`.
Returns -1 if the `item` is not found.
If the `item` is present more than once, the `indexOf` method returns the position of the first occurence.

7. Pipeline

An interesting aspect of the `reduce method` in `JavaScript` is that you can `reduce` over `functions` as well as `numbers` and `strings`.
Let’s say we have a collection of simple mathematical `functions`. These `functions` allow us to increment, decrement, double and halve an amount.

The problem is that we know we are going to need to increment the amount three times, then double it, then decrement it. We don’t want to have to rewrite our `function` every time so we going to use `reduce` to create a `pipeline`.

```js
const increment =  input => input + 1;
const decrement = input => input - 1; 
const double = input => input * 2; 
const halve = input => input / 2; 
```

A pipeline is a term used for a `list of functions` that transform some `initial value` into a `final value`. Our pipeline will consist of our three `functions` in the order that we want to use them.

```js
const pipeline = [increment, double, decrement]
```

Instead of `reducing` an `array of values` we `reduce` over our `pipeline of functions`. This works because we set the `initial value` as the `number` we want to transform.

```js
const increment =  input => input + 1;
const decrement = input => input - 1; 
const double = input => input * 2; 
const halve = input => input / 2; 

const pipeline = [increment, double, decrement]

const result = pipeline.reduce((acc, func) => {
   return func(acc)
}, 1)


console.log(result) // 3
```
Because the pipeline is an `array`, it can be easily modified. If we want to decrement something three times, then double it, decrement it , and halve it then we just alter the pipeline. The `reduce function` stays exactly the same.

```js
var pipeline = [
  increment,
  increment,
  increment,
  double,
  decrement,
  halve
];
```

### Silly Mistakes to avoid

If you don’t pass in an `initial value`, `reduce` will assume the `first item` in your `array` is your `initial value.` This worked fine in the first few examples because we were adding up a list of numbers.

If you’re trying to count the `frequency` of the `fruit`, and you leave out the `initial value` then things get weird. Not entering an `initial value` is an easy mistake to make and one of the first things you should check when debugging.

Another common mistake is to forget to `return` the `accumulator/initial value`. You must `return` something for the `reduce function` to work. Always double check and make sure that you’re actually `returning` the` value` you want.



















