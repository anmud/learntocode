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

