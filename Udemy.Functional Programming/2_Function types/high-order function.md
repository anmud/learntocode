# High-order function

`High-order function` is a function that either takes a `function` as an `input parameter` and/or returns a `function`. 

```js
function myFunction(fn){
    return function(){
        .....
    }
}
```

### Closure 

`Closures` are `functions` that can access and use `variables` that are not directly passed into the `function`, because of the placement of the function relative to the `variables`. The parameter `'greeting'` can be used anywhere between the openning and closing the curly braces of the `'greet()' function`. this is the `scope` of the `parameter`. Since the `return function` is in this `scope`, it has access to the `'greeting'` parameter. 

```js
 function greet(greeting) {
     return function(name){
         return `${greeting} ${name}`
     }
 }

 const friends = ['Nate', 'Jim', 'Scott', 'Dean']
 const friendsGreetings = friends.map(greet('Good morning'));
 console.log(friendsGreetings) // ['Good morning Nate', 'Good morning Jim', 'Good morning Scott', 'Good morning Dean']

 ```
 ### Exersise

 ```js
 // create the code to go from studentGrades array, 
// to studentFeedback (as shown in comments below)

const studentGrades = [ 
  {name: 'Joe', grade: 88},
  {name: 'Jen', grade: 94},
  {name: 'Steph', grade: 77},
  {name: 'Allen', grade: 60},
  {name: 'Gina', grade: 54},
];


/*
const studentFeedback = [
  'Nice Job Joe, you got an b',
  'Excellent Job Jen, you got an a',
  'Well done Steph, you got an c',
  'What happened Allen, you got an d',
  'Not good Gina, you got an f',
]; 
*/
```