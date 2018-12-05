# Updating objects in an immutable way

### To update existing property in the object

Use `spread operator (...)`. If you want to update the `existing property` use the new `value` of a `property` after the `spread operator`. 

```js

const meal = {
description: 'breakfast',
id: 1
}

const updatedMeal = {
...meal,
description: 'snack'                       
} 

console.log(updatedMeal) // output:  {description: 'snack', id: 1}
```

### To add one more property to the object

Also use `spread operator (...)`. If you want to add a `new property`, use the new  `property` after the `spread operator`. 

```js
const updatedMeal = {
...meal,
calories: 600                                    
}

console.log(updatedMeal) // output: { description: 'breakfast', id: 1, calories: 600}
```

## Exersise

```js
const meal = {
  description: 'Dinner',
};
// 1. In an Immutable way, add a property to the
// meal called calories setting it's value to 200,
// then log the result to the console

const mealWithCalories = {
  ...meal,
  calories: 200
};

console.log(mealWithCalories); // { calories: 200, description: "Dinner"}

// 2. In an Immutable way, increase the calories 
// by 100 and print the result to the console

const mealWithIncreasedCalories = {
  ...mealWithCalories,
  calories: mealWithCalories.calories + 100,
};

console.log(mealWithIncreasedCalories); // {calories: 300, description: "Dinner"}

// 3. In an Immutable way, remove the calories property and log the result to the console

const {calories, ...mealWithOutCalories} = mealWithIncreasedCalories;

console.log(mealWithOutCalories); // {description: "Dinner"}
```
