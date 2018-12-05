# Deleting a property from an object in an immutable way 

To delete a property from an object we'll nee two things: `destructuring` and `rest syntax`

1. First destructure
```js
const updatedMeal = {
id: 1,
description: 'snack',
calories: 600                      
}

const {description, calories, id} = updatedMeal // destructuring

console.log(updatedMeal) //  snack, 600, 1
```
2. Then to delete item we'll use rest syntax 

```js
const { Id,   ...mealWithoutId} = updatedMeal
```

