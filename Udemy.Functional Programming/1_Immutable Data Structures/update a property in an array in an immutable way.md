# Update the property in an array in an immutable way

How can you update a `property` in an array in an `immutable way`? 

To update: use `map() function`

Let's change the description under id2 in updatedMeals

```js

const updatedMeals = [
{id: 1, description: "breakfast", calories: 200},  -  this represents a meal 
{id: 2, description: "lunch", calories: 400},    -  this represents a meal 
{id: 3, description: "snack", calories: 150}   -  this represents a meal  
]

const updatedMealsDescription = updatedMeals.map(updateDescription)

function updateDescription(meal){
if( meal.id  === 2 ){return {
...meal,
description: "Early lunch"
}
};
return meal;
}
```

### Exersise

```js
// 1. create a constant named friends, which is an array that contains 2 names of your choosing.

const friends = ['Nate', 'Michael'];

// 2. Create a new constant named updatedFriends, which includes the friends array values plus one additional name

const updatedFriends = [...friends, 'Dustin'];

// 3. Create a new constant named friendNameLengths, which is based on the array updatedFriends, but instead of having the friends names, have the array store the length of each persons name.

const friendNameLengths = updatedFriends.map(nameToLength);

function nameToLength (name) {
  return name.length;
}

// 4. Create a new constant named shorterNamedFriends, which will be a list of the friends except the friends with the longest name.
const maxFriendLength = Math.max(...friendNameLengths);

const shorterNamedFriends = updatedFriends.filter(
  function(name){
    return name.length < maxFriendLength ;
  });

// 5. Print each constant to the console.

console.log(friends, updatedFriends, friendNameLengths, shorterNamedFriends);
// ["Nate", "Michael"]
//["Nate", "Michael", "Dustin"]
//[4, 7, 6]
//["Nate", "Dustin"]
```



