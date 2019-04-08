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

## A `data model`

A `model` defines e.g an object, an array or simple data types) that a user can see and interact through a user interface. 
```js
const dataModel = [
{name: "Anastasia", city: {"Berlin"}, countryCode: 49},
{name: "John Doe", city: {"San Francisco"}, countryCode: 1}
]
```
A `data model` is the same as `state`.
What is an `application state`? A place where you store a `data model`. Also a `state` is what an application has to remember. Such as add new things to the model, delete new things from the model, update things in the model.