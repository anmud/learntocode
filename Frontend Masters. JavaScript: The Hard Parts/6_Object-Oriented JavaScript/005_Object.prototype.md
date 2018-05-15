# `Object.prototype`

**Complete Solution 3**

```js
function User(name, score){
this.name = name;
this.score = score;
}
User.prototype.increment = function(){
this.score++;
};
User.prototype.login = function(){
console.log("login");
};
let user1 = new User(“Eva”, 9)
user1.increment();
```

### Line-by-line

1. declare a function `User`
***Remember*** `User`function is also an `object`. This `object` has automatically a property - `prototype` , which is itself an `object`. 

`User { prototype : {} }`

3. now to our `prototype object` we add property `inctement` with the `value` of a whole `function` definition

`User { prototype : {increment : function(){ console.log("login"); }; } }`

4. now to our `prototype object` we add property `login` with the `value` of a whole `function` definition

`User { prototype : {login : function(){ console.log("login"); } }`

5. create a `variable` called `user1` , for now it is undefined, we don't know what it is gonna return
6. we call `User` function, pass `arguments` and create a new `execution` context
7. we push our `User` function to the `call stack`
we say:"whatever will be returned from the `User` function, assign it to the `user1`"
8. we run our `User` function with `new` keyword 
9. in the new `execution context` the `new` keyword will **automatically** do for us the steps inside the `function`:
- creates an empty `object` 
- and assigns this empty `object` to label `this` !!!!!!!!!!!!!!!!!!!!
- the `User` function's context has been set to an empty `object` `this` 
-  by default `this` object is gonna link to `User.prototype` which is just an `object` (inside the `User` object), and which itself has an `increment` property with a `function` 
10. now (manually) in our empty object `this` we add the property `name` with the value `'Eva'`, and a property `score` with the value `9`
11. again **automatically:** `return this`  

it `returns {name:Eva, score:9, _proto_ which is pointing to User.prototype }`
12. we store the returned `value` in `user1` 

`user1 = {name:Eva, score:9, _proto_ which is pointing to User.prototype }`

