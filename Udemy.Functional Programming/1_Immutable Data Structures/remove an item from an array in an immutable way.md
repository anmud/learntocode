# Remove an item from an array in immutable way

How to remove an `item` from an `array` in an `immutable way`?

Use `filter() function`: e.g
```js

const updatedMeals = [
{id: 1, description: "breakfast", calories: 200},  -  this represents a meal 
{id: 2, description: "lunch", calories: 400},    -  this represents a meal 
{id: 3, description: "snack", calories: 150}   -  this represents a meal  
]


const filteredMeals = updatedMeals.filter(function(meal){
return meal.id !== 1
});


updatedMeals = [
{id: 2, description: "lunch", calories: 400},   
{id: 3, description: "snack", calories: 150}   
]
```

