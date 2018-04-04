Scope determines the accessibility (visibility) of variables.

# JavaScript Function Scope

In JavaScript there are two types of scope:

* Local scope
* Global scope

JavaScript has function scope: Each function creates a new scope.

Scope determines the accessibility (visibility) of these variables.

Variables defined inside a function are not accessible (visible) from outside the function.

## Local JavaScript Variables

Variables declared within a JavaScript function, become LOCAL to the function.

Local variables have local scope: They can only be accessed within the function.

### Example
```js
// code here can not use carName

function myFunction() {
    var carName = "Volvo";

    // code here can use carName

}
```
Since local variables are only recognized inside their functions, variables with the same name can be used in different functions.

Local variables are created when a function starts, and deleted when the function is completed.

## Global JavaScript Variables

A variable declared outside a function, becomes GLOBAL.

A global variable has global scope: All scripts and functions on a web page can access it. 

### Example

```js
var carName = " Volvo";

// code here can use carName

function myFunction() {

    // code here can use carName 

}
```
