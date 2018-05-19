# Class Syntactic

**Solution 4**
We’re writing our shared `methods` separately from our object `constructor` itself (off in the User.prototype object). Other languages let us do this all in one place. ES2015 lets us do so too.

**The class ‘syntactic sugar’**

```js
class User {
constructor (name, score){
this.name = name;
this.score = score;
}
increment (){
this.score++;
}
login (){
console.log("login");
}
}
let user1 = new User("Eva", 9);
user1.increment();
```
### Line-by-line

1. declare a `class` (it has two parts)
2. in the first part we create a constructor `function`
3. `increment` get stored in `User` prototype
4.  `login` get stored in `User` prototype
5. ..

#### Benefits:
— Emerging as a new standard
— Feels more like style of other languages (e.g. Python)

#### Problems
— 99% of developers have no idea how it works and therefore fail interviews