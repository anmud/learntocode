# The `break` Statement

```js
while (true) {
  // this is an endless loop
  break;
  // but break, lets you "break out" of the loop
}
```
**Resources**

[The break statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/break) on the Mozilla Developer Network

### Example

```js 
var randomNumber = getRandomNumber(10);
var guess;
var guessCount = 0;
var correctGuess = false;

function getRandomNumber( upper ) {
  var num = Math.floor(Math.random() * upper) + 1; 
  return num;
}

while (true) //here to have true condition is a bad idea, cos the code will run forvever, but for the example we have the break statement.
  guess = prompt('I am thinking of a number between 1 and 10. What is it?');
  guessCount += 1;
  if (parseInt(guess) === randomNumber) {
    correctGuess = true;
    break; 
  }  
} 
  
document.write('<h1>You guessed the number!</h1>');
document.write('It took you ' + guessCount + ' tries to guess the number ' + randomNumber);
``` 
We can change this game so, that it is allowed only `10` guesses. The simple way to do that would be to use the `for` loop or `while` loop with a counter `variable` to keep track of the number of guesses. 

```js 
var randomNumber = getRandomNumber(10);
var guess;
var guessCount = 0;
var correctGuess = false;

function getRandomNumber( upper ) {
  var num = Math.floor(Math.random() * upper) + 1; 
  return num;
}

while ( guessCount < 10 ) //here we have the allowed number of guesses 
  guess = prompt('I am thinking of a number between 1 and 10. What is it?');
  guessCount += 1;
  if (parseInt(guess) === randomNumber) {
    correctGuess = true;
    break; 
  }  
} 
  
document.write('<h1>You guessed the number!</h1>');
document.write('It took you ' + guessCount + ' tries to guess the number ' + randomNumber);
``` 
Now the `loop` will either run `10` times or if the user guesses the correct number first, the `loop` ends because of the `break` statement. 

Then we can use a `conditional` statement to check the user correctly guess the number. 

```js 
var randomNumber = getRandomNumber(10);
var guess;
var guessCount = 0;
var correctGuess = false;

function getRandomNumber( upper ) {
  var num = Math.floor(Math.random() * upper) + 1; 
  return num;
}

while ( guessCount < 10 ) //here we have the allowed number of guesses 
  guess = prompt('I am thinking of a number between 1 and 10. What is it?');
  guessCount += 1;
  if (parseInt(guess) === randomNumber) {
    correctGuess = true;
    break; 
  }  
} 
if(correcctGuess){            //we use the conditional statement
  document.write('<h1>You guessed the number!</h1>');
document.write('It took you ' + guessCount + ' tries to guess the number ' + randomNumber);
} else {
    document.write('<h1>Sorry, you didn\'t guess the right number.</h1>');
}
``` 
