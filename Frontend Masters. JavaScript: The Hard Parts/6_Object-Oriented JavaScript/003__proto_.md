# _proto_

**Using the `prototypal nature` of JavaScript - Solution 2 in full**

```js
function userCreator (name, score) {
let newUser = Object.create(userFunctionStore);
newUser.name = name;
newUser.score = score;
return newUser;
};
let userFunctionStore = {
increment: function(){this.score++;},
login: function(){console.log("You're loggedin");}
};
let user1 = userCreator("Will", 3);
let user2 = userCreator("Tim", 5);
user1.increment();
```

### Line-by-line

1. declaring a function `userCreator`
2. create a variable `userFunctionStore`  - and assign  an object to it
-  first `property` of this `object` is `increment` with the value of a `function`, second - `login` also  with the value of a `function`
3. declare `user1` and we assign to it the returned `value` of `userCreator` function - in our case it will be some sort of object, but we don't know it yet, so, the result will be `ubdefined`
4. we call `userCreator`, pass `arguments` and open new execution context
5. push `userCreator` to the `call stack`
6. into our local memory goes `'Will'`parameter - assigned to the label `name`, and `'3'` parameter assigned to the label `score`
7. inside of a new context we declare a `newUser` and create an empty `object` in it.

**NOTE** Whenewer we pass in to our parameters on `Object.create` , we gonna have in our empty `object` somehow a special 
`bond` to the thing we passed in, in our case - the function `userFunctionStore` 

8. we create a new property  `name` assign an input argument `Will` to it.  
9. create a new property `score` and assign an input argument `3` to it
10. return `newUser` object and store it in `user1` 
11. declare `user2` and have all the previous steps as with the `user1` 
12. `user1.increment()` - first welook for `user1` and we find it - this is now an `object` with two properties: name, score
13. then we look for `inctement` and we don't find it in the `user1` object
14. now we look at our special `bond` (`_proto_`) which has a reference to `userFunctionStore` object and we find here `increment` property which has some functionality to run. 
15. we create an `execution context` to run that functionality
16. we add `user1.increment` to the `call stack`
17.  the code says `this.score ++` 

**NOTE** Actually, `increment` function ca be used by all the `objects` we return. How can we make shure when we run `inctrement` function, we are referring to the right obect? We use the keyword `this`. And the keyword `this` is like a placeholder. And actually whenever we create `execution context`, we fill in any variables and argument AND JavaScript always also assign the value of `this`. 
*Our basic fundamental rule is*  - the `ths` refer inside the `execution context` to whatever is the `left of the dot` where that `function` is being called upon. 

18. so `this` is gonna be filled with `user1`
19. first we look for `user1` in lockal context, we don't find
20. we go to global, find it and `increment` `3`  

the bond (`_proto_`) is known as - `prototype setting bond`. 