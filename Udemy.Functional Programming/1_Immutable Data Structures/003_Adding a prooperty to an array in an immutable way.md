# Add a property to an array in a immutable way

How can you add one more `property` to an `array` in an `immutable way`? 

Use `spread operator`. To add one more property, e.g:

```js
const meals =[ 
{id: 1, description: "breakfast", calories: 200},
{id: 2, description: "lunch", calories: 400},
]

const meal = {
id: 3,
description: "snack",
calories: 150
}

const updatedMeals = [...meals, meal] //add after the spread operator

updatedMeals = [
{id: 1, description: "breakfast", calories: 200},
{id: 2, description: "lunch", calories: 400},
{id: 3, description: "snack", calories: 150}
]
```