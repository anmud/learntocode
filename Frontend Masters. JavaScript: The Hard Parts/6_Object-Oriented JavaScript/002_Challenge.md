# Challenge OOP

**Working with Object Literals**

#### Challenge 1/1
Create a `function` that accepts two `inputs` (name and age) and returns an `object`. Let's call this function `makePerson`. This function will:
- create an empty `object`
- add a `name` property to the newly created `object` with its `value` being the `name` argument passed into the `function`
- add an `age` property to the newly created `object` with its value being the `age` argument passed into the `function`
- return the `object`


### **Using Object.create**

#### Challenge 1/3
- Inside `personStore` object, create a property `greet` where the `value` is a `function` that logs `"hello"`.
#### Challenge 2/3
- Create a function `personFromPersonStore` that takes as input a `name` and an `age`. When called, the `function` will create `person` objects using the `Object.create` method on the `personStore` object.
#### Challenge 3/3
- Without editing the code you've already written, add an `introduce` method to the `personStore` object that logs `"Hi, my name is [name]"`.

### Solution

```js

/*** CHALLENGE 1 of 1 ***/

function makePerson(name, age) {
	// add code here
let newPerson = {};
  newPerson.name = name;
  newPerson.age = age;
  return newPerson;
}


var vicky = makePerson('Vicky', 24);

console.log(vicky.name); // -> Logs 'Vicky'
console.log(vicky.age); // -> Logs 24

/****************************************************************
                       USING OBJECT.CREATE
****************************************************************/

/*** CHALLENGE 1 of 3 ***/

var personStore = {
	// add code here
  greet : function (){console.log('Hello')}

};

personStore.greet(); // -> Logs 'hello'



/*** CHALLENGE 2 of 3 ***/

function personFromPersonStore(name, age) {
	// add code here
let person = Object.create(personStore);
person.name = name;
person.age = age;

return person; 
}

var sandra = personFromPersonStore('Sandra', 26);


console.log(sandra.name); // -> Logs 'Sandra'
console.log(sandra.age); //-> Logs 26
sandra.greet(); //-> Logs 'hello'



/*** CHALLENGE 3 of 3 ***/

personStore.introduce = function(){console.log('Hi, my name is ' + this.name)};


sandra.introduce(); // -> Logs 'Hi, my name is Sandra'
```
