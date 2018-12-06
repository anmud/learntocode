# Curring and Partial Application

`Currying` - the transformation from a `function` with multiple `arguments` to a `function` that takes a `single argument` and returns a `function` that takes the remaining `argument`. This is what you do to a `function` before you actually use that `function` (what's done while designing/coding a function).

`Partial application` - specializing a more general `function`. This is what's done when you begin to use the `function` in part by applying some of the `parameters` the `function` needs, but not all of them. It is what you are doing when you use a `curryied function`.

Can you do the `partial application` without a `curryied function`? Well, yes. We can use `helper function` which performs the `partial application` on a `regular old function` (a `non-curryied function`). 

### Examle
```js
//partial: allows for partial application

function add(x,y){         //regular function
    return x + y
}

const add3 = partial(add, [3]); //we pass the first argument; this is a partial application, what's returned with partial is a new function that needs to be called with the last parameter

console.log(add3(2)); // we pass the second parameter by calling add3 with an argument; result => 5
```

Well, `currying` is related to creating `functions`, and when you are currying there is an `absence of data`. `Partial application` is related to consuming or using `functions` `with actual data`! You can use `partial application` with `curried functions` or `regular functions` with some sort of `helper function`.

## Parameters order

If we use `currying` does the order of `parameters` for the create function matter? 
Any `parameter` that turns in more `general function` and in more `specialized function` should be the first `parameters`. The last `piece of data` should be a piece of data your `function` is acting on (data on what map() function works). 

```js
['Nate', 'Jim'].map(greet('Good morning')) // greet function is acting on the individual name of the list that is passed ; 
//in orther words we created greet function for the name, so the name is the data the function is acted on
```

## Lambda syntax

Use `Ramda` [library](https://ramdajs.com/). We can use it by pasting the `<script> tag` in the head of the HTML file.
Let's write `greeting function` with the rambda library. Now we'll not use the `function keyword` to create a function, instead we;ll use alternative syntax, which is called `'fat arrow function syntax'` or `'lambda syntax'` ( `() => {}` ). 

```js

const greet = (greeting, name) => `${greeting} ${name}`;
```

In this example we dont' use the `return keyword` as well as the curly braces `{}` after the arrow `=>`, the `return value` is implicit . This function is not different from the `original function`: 

```js
function greet(greeting, name){
    return `${greeting}  ${name}`
}
```

But if we call `rambda's curry function` passing this new function ("const greet = (greeting, name) => `${greeting} ${name}`") as a parameter to the `curry function`, what's return by the `curry function` is a new `curryied version` of this function, which we'll be able to use in a much more pleasant way. 

The `ramda functions` are available on the `R.global`. So we can call `const greet = R.curry` and then wrap the whole `function` in the parenthesis.

```js

const greet = R.curry((greeting, name) => `${greeting} ${name}`);
```

