# Destructuring

What is destructuring? 

You can take out elements from an `array` or an `object` and assign them to `variables`.
`Destructuring`, a convenient way to extract `values` from `data` stored in (possibly nested) `objects` and `arrays`. 

```js
const arr = ["first", "second", "third"]
const obj = {a: "value of a", b: "value of b", c: "value of c"}

// when we destructure an array we can assign random variable names
const [first, second, third] = arr

// when we destructure an object we need to take keys as variables names
const {a, b, c} = obj


console.log(
  first,
  second,
  third,
  a,
  b,
  c
  )
//result array destructuring - first second third 
//result object destructuring - value of a value of b value of c
```

### Example

```js
const state = ["first value", (x => x + "!!! this gets added")]

// we take out the values based on the order inside the array
const [first1 , second2] = state

console.log(second2(first1))
//result - first value!!! this gets added
```

### Example

```js

makeSound({
  //species: "dog",
  weight: "23",
  sound: "woof"
})

function makeSound(options){
  let {species, sound} = options
  species = species || "animal"
  console.log("The " + species + " says " + sound + "!")
}

//result - "The animal says woof!"
```

### OR we can do it even shorter if we destructure the object in the method signature and assign default values in it.

```js
makeSound({
  //species: "dog",
  weight: "23",
  sound: "woof"
})

function makeSound({species = "animal", sound})
  console.log("The " + species + " says " + sound + "!")
}

//result - "The animal says woof!"
```

## `Rest` and `spread` operator

What are a `rest` and  a `spread operators` in JS? 

- `Spread operator` comes after an `=` (equal sign)
It spreads the elements of the `object` into a `new object`
- `Rest operator` comes before an `=` (equal sign)
It gathers `rest of elements` into a `new object`

```js
// here we added a new property to a newly created object newMeal. The new property is called total
const newMeal = {...meal, total: 1100}  //spread 

const updatedTotal = {
  ...newMeal,
  total: 1000
}

// we create here a new object from meal that is called mealWithoutDinner, this new object does not contain dinner as a property anymore.
const {dinner, ...mealWithoutDinner} = meal  //rest
```

### More `spread` examples

1. 
```js
const movies = ["Leon", "Love Actually", "Lord of the Rings"];

console.log(...movies)
//result - "Leon", "Love Actually", "Lord of the Rings"

//combine two arrays together 
const shapes = ["triangle", "square", "circle"];
const objects = ["pencil", "notebook", "eraser"];

const chaos = [...shapes, ...objects]

console.log(chaos)
//result -  ["triangle", "square", "circle", "pencil", "notebook", "eraser"]

```
2. Add the elements of an existing array into the new array

```js
const certsToAdd = ['Algorithms and Data Structures', 'Font End Libraries'];
const certifications = ['Responsive Web Design', ...certsToAdd, 'Data Visualisation', 'APIs and Microservices', 'Quality Assurance and Information Security'];

console.log(certifications)
//result - ["Responsive Web Design", "Algorithms and Data Structures", "Font End Libraries", "Data Visualisation", "APIs and Microservices", "Quality Assurance and Information Security"]
```

3. Pass elements of an array as arguments into a function

```js

function addThreeNumbers(x,y,z){
console.log(x+y+z)
}

const args = [0,1,2]
addThreeNumbers(...args)

//result - 3
```

4. Copy arrays

```js
const arr = [1,2,3]
const arr2 = [...arr]
arr2.push(4)

console.log(arr, arr2)
//result - (3) [1, 2, 3]  (4) [1, 2, 3, 4]
```
5. Change value inside the array object

```js
const users = [
    {name: "Anastasia", city: "Berlin", countryCode: 49, id: 1},
    {name: "John Doe", city: "San Francisco", countryCode: 1, id: 2}
    ]

const changeCity = users => users.map(changedCity)
const changedCity = user => {
  const {name}  = user
  if(name === "Anastasia"){
    return {...user, city: "Los Angeles"}
  } else return user
}

console.log(changeCity(users))
// result - 
//0: {name: "Anastasia", city: "Los Angeles", countryCode: 49, id: 1}
//1: {name: "John Doe", city: "San Francisco", countryCode: 1, id: 2}
```


### More `rest` examples
1. 
```js
const movie = ["Life of Brain", 8.1, 1979, "Graham Chapman", "John Cleese", "Michael Palin"]

const [title, rating, year, ...actors] = movie

//Thanks to the rest parameter, actors gets assigned the remaining values of the movie array, in form of an array.

console.log(title,rating,year,actors)
//result - Life of Brain 8.1 1979 (3) ["Graham Chapman", "John Cleese", "Michael Palin"]
```
2.  In the `function` we gonna pass in two arguments: multiplier and the argument that has the rest operator (where actually we can pass as many arguments as we want), well the firts argument is `multiplier` and the rest we pass in will be condenced into the array called `theArgs`. Since it is an array we can use array methods like `map`. Now its gonna multiply each element in theArgs by the multiplier. So, in our example `const arr = multiply(2,1,2,3);` - 2 is the multiplier and the rest elements are the array. 

```js
function multiply(multiplier, ...theArgs){
  return theArgs.map(function(element){
    return multiplier * element;
  });
}
const arr = multiply(2,1,2,3);
console.log(arr)
//result - [2,4,6]
```
3. Transforming the given array and adding and removin properties from each object

```js
const songs = [
  {id: 1, name: "Curl of the Burl", artist: "Mastodon"},
  {id: 2, name: "Oblivion", artist: "Mastodon"},
  {id: 3, name: "Flying Whales", artist: "Gojira"},
  {id: 4, name: "L'Enfant Sauvage", artist: "Gojira"}
]

const mapped = songs.map(song => {
  //first we remove the artist property
  const {artist, ...rest } = song
  //return a new object without artist property and with two new properties being added
  return {
    ...rest,
    scrobbleCount: 0,
    spotifyUrl: "let's just imagine these properties make sense for now",
  }
})

console.log(mapped)
//result : 
// 0: {id: 1, name: "Curl of the Burl", scrobbleCount: 0, spotifyUrl: "let's just imagine these properties make sense for now"}
// 1: {id: 2, name: "Oblivion", scrobbleCount: 0, spotifyUrl: "let's just imagine these properties make sense for now"}
// 2: {id: 3, name: "Flying Whales", scrobbleCount: 0, spotifyUrl: "let's just imagine these properties make sense for now"}
// 3: {id: 4, name: "L'Enfant Sauvage", scrobbleCount: 0, spotifyUrl: "let's just imagine these properties make sense for now"}
```


## A `data model`

A `model` defines e.g an object, an array or simple data types that a user can see and interact through a user interface. 
```js
const dataModel = [
{name: "Anastasia", city: {"Berlin"}, countryCode: 49},
{name: "John Doe", city: {"San Francisco"}, countryCode: 1}
]
```
A `data model` is the same as `state`.
What is an `application state`? A place where you store a `data model`. Also a `state` is what an application has to remember. Such as add new things to the model, delete new things from the model, update things in the model.