# Intro

OOP - an enormously popular paradigm for structuring our complex code.
- easy to add features and functionality 
- performant (effecient in terms of memory)
- easy for us and other developers to reason about (a clear ctructure)

`Objects` - store functions with their associated data!
```js
let user1 = {
name: "Will",
score: 3,
increment: function() {
user1.score++;
}
};
user1.increment(); //user1.score => 4
```
Encapsulation - binding together the `data` and `functions` that manipulate the `data`.

### **What alternative techniques do we have for creating objects?** 

#### `.dot notation`

Creating user2 user `dot notation`
```js
let user2 = {}; //create an empty object
user2.name = "Tim"; //assign properties to that object
user2.score = 6;
user2.increment = function() {
user2.score++;
};
```

### `object.create`

Creating user3 using `Object.create`
```js
let user3 = Object.create(null);
user3.name = "Eva";
user3.score = 9;
user3.increment = function() {
user3.score++;
};
```
Our code is getting repetitive, we're breaking our DRY principle. And suppose we have millions of users!
What could we do?

**Solution 1. Generate objects using a function**

```js
function userCreator(name, score) {
let newUser = {};
newUser.name = name;
newUser.score = score;
newUser.increment = function() {
newUser.score++;
};
return newUser;
};
//later
let user1 = userCreator("Will", 3);
let user2 = userCreator("Tim", 5);
user1.increment();
user2.increment();
```
#### **Problems:**
Each time we create a new user we make space in our computer's memory for all our data and functions. But our functions are just copies.

Is there a better way?

#### **Benefits:**
It's simple!


**Solution 2.**

Store the `increment function` in just one `object` and have the interpreter, if it doesn't find the `function` on
`user1`, look up to that `object` to check if it's there. 
How to make this link?
