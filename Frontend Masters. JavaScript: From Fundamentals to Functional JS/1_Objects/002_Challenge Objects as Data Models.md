# Objects as Data Models

This object will be the model of a single animal user. Extra points if you get the pun in the last sentence.

**Object**

An object to hold our data model...

1. Create a variable, name it animal, and assign it an object literal.

*With Dot Notation…*

2. Add a property called username and assign it a value.
3. Ensure that your username property exists in animal by inspecting it in the console.

*With Bracket Notation…*

4. Add a property called tagline and give it a value.
5. Check that your property exists in the animal object by inspecting it in the console.
6. Create a variable called noises and assign it an empty array []
7. Add the noises array to your object.
8. Inspect your handiwork! Your object should look something like this:
  `{ username: 'DaffyDuck', tagline: 'Yippeee!', noises: [] }`

**Loops**

9. Loop through the properties of your animal object.
10. Count everytime it loops to keep track of the number of properties on your object.
11. Write an if/else statement in your loop:
-  If the key is username, console.log('Hi my name is ' + ___) //fill in with object's username value.
-  If the key is tagline, console.log('I like to say ' + ___) //fill in with object's tagline value.
12. What happens if you return 'Hi my name is ' + ___ instead of using console.log() inside the loop?

### Solution
```js
var animal = {

}

animal.username  = "Ana Mo";
animal.tagline = "Hug me!";
let noises = [ ];
animal['noises'] = noises;  

console.log(animal);
let count = 0;

for(let property in animal){
count ++;
if(property === 'username'){  
console.log("Hi,My name is " +  animal[property]);
}else if(property === 'tagline'){
console.log("I like to say " + animal[property]);
}
}
```
**Review**

Let's go over some concepts:

* What are the different ways you can add properties and values to objects?
answer: the loop will end after the first iteration
* Which of these methods would you use if you wanted to add a property to an object that had a weird symbol (think '&')?
answer: dot notation and bracket notation
* What about if the property is a variable, how does that change the syntax?
answer: should use bracket notation
* Which of these methods would you use if you wanted to add a property to an object that had a weird symbol (think '&')?
answer: use bracket notation and quotes