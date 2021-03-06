# Pure functions vs procedures

### A pure function - a `function` that maps `arguments` to results.

```js
function double(num) {
  return num * 2
}

console.log(double(10))
//result - 20
```

### An impure function - a `function` as `procedure` - `function` with side-effect.

In the example below the `function` "user" reassigns a new value to "count" `variable`, that is out of the `scope` of the `function` itself.

```js
let count = 0

function user(num) {
  count = count + num
}

console.log(user(10),
  		    count)
// result - count itself was changed to 10 

function check(countValue) {
  if (countValue === 0) {
    return "success"
  } else {
    return "error"
  }
}
console.log(check(count))
//result - "error", cos the count itself was already changed to 10 
```
### One more example of a pure function

```js
const permissions = {
  isAdmin: true,
  name: "Anastasia",
}

// 1. function gets called
// 2. first argument of this function gets parametarized, means the passed arguments in this case "permissions" variable, becomes "user" parameter in the function.
// pure function: maps arguments to results

function checkPermission(user) {
  const isAdmin = user.isAdmin
  const name = user.name
  
  if (isAdmin) {
    return "success"
  } else {
    return "error"
  }
}

console.log(
    checkPermission({isAdmin: true, name: "Anastasia"}),
  	checkPermission(permissions),
)
//result - "success"
//result - "success"
```

In `const` variable if it is an `object` or `array`. You can still change the properties.

```js
const user2 = {name: "Anastasia"}

// pure function: maps arguments to results
function getName(user2){
  const name = user2.name
  return name
}

console.log(getName(user2))
//result - "Anastasia"

// function as procedure (function with side-effect)
function changeName(user2){
  const name = user2.name
  user2.name = "Dimitri"
  return user2
}

console.log(
  		changeName(user2),
  		user2
)
//result - {name: "Dimitri"}
```

### Example

```js
// race is in the global scope, and can be accessed/modified by any functions
const race = "100m Dash"
const winners = ["Hunter Gath", "Singa Song", "Imda Bos"];


// in parens (winner , i, array) are called parameters
const make = (winner, i, array) => ({name: winner, race: race, place: i + 1})

//const win = winners.map(make) - behind the scenes
// const win = winners.map(make(winner[0], 0))
// const win = winners.map(make(winner[1], 1))
// const win = winners.map(make(winner[2], 2))
const win = winners.map(make)
// win function is impure


const pureWin = (winners, race)=> {
  const result = winners.map((winner, i) => ({name: winner, race: race, place: i +1}))
  return result
}

const result = pureWin(winners, race)

console.log(
  win,
  result,
)

//result [{...}, {...},{...}]
//0: {name: "Hunter Gath", race: "100m Dash", place: 1}
//1: {name: "Singa Song", race: "100m Dash", place: 2}
//2: {name: "Imda Bos", race: "100m Dash", place: 3}
```
