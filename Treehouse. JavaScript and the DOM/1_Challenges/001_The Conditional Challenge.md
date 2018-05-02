# The Conditional Challenge 

## Challenge Instructions (a quizz)

1. Ask a player at least five questions

2. Keep track of the number of questions the user answered correctly

3. Provide a final message after the quiz letting the user know the number of questions he or she got right.

4. Rank the player. If the player answered all five correctly, give that player the gold crown: 3-4 is a silver crown; 1-2 correct answers is a bronze crown and 0 correct is no crown at all.

## Solution 1 

```js
var score = 0;
var question1 = prompt('Do camels store water in their humps?').toLowerCase()
var answer1 = 'no';

if(question1 === answer1){
  score += 1;
  alert('Your answer is right!');
} else if (question1 !== answer1){
  score = 0 ;
  alert('Wrong!');
} 

var question2 = prompt('What is a baby kangaroo called?').toLowerCase()
var answer2 = 'a joey';

if(question2 === answer2){
  score++ ;
  alert('Your answer is right!');
} else if (question2 !== answer2){
  var newScore = 0;
  alert('Wrong!');
} else if (newScore === 0){
  score = 1;
} 
  

var question3 = prompt('What is the tallest animal in the world?').toLowerCase()
var answer3 = 'a giraffe';

if(question3 === answer3){
  score ++;
  alert('Your answer is right!');
} else if (question3 !== answer3){
  var newScore = 0;
  alert('Wrong!');
} else if (newScore === 0){
  score = 2;
}

var question4 = prompt('Are all types of snakes poisonous?').toLowerCase()
var answer4 = 'no';

if(question4 === answer4){
  score ++ ;
  alert('Your answer is right!');
} else if (question4 !== answer4){
  var newScore = 0;
  alert('Wrong!');
} else if (newScore === 0){
  score = 3;
}

var question5 = prompt('What is a baby cow called?').toLowerCase() 
var answer5 = 'a calf';
if(question5 === answer5){
  score++ ;
  alert('Your answer is right!');
} else if (question5 !== answer5) {
  var newScore = 0;
  alert('Wrong!');
} else if (newScore ===0){
  score = 4;
}

alert('You gave ' + score + ' right answers');

if (score === 5){
  alert('You won the gold crown!');
} else if (score === 3 || score === 4){
  alert('You won the silver crown!');
} else if (score === 1 || score === 2){
  alert('You won the bronze crown!')
} else {
  alert('You are a looser!');
}
```

## Solution 2 (more beautiful and easy)

```js
// quiz begins, no answers correct
var correct = 0;

// ask questions
var answer1 = prompt("Name a programming language that's also a gem");
if ( answer1.toUpperCase() === 'RUBY' ) {
 correct += 1; 
}
var answer2 = prompt("Name a programming language that's also a snake");
if ( answer2.toUpperCase() === 'PYTHON' ) {
 correct += 1; 
}
var answer3 = prompt("What language do you use to style web pages?");
if ( answer3.toUpperCase() === 'CSS' ) {
 correct += 1; 
}
var answer4 = prompt("What language do you use to build the structure of web pages?");
if ( answer4.toUpperCase() === 'HTML' ) {
 correct += 1; 
}
var answer5 = prompt("What language do you use to add interactivity to a web page?");
if ( answer5.toUpperCase() === 'JAVASCRIPT' ) {
 correct += 1; 
}

// output results
document.write("<p>You got " + correct + " out of 5 questions correct.<p>");

// output rank
if ( correct === 5 ) {
  document.write("<p><strong>You earned a gold crown!</strong></p>");  
} else if (correct >= 3) {
  document.write("<p><strong>You earned a silver crown.</strong></p>");  
} else if (correct >= 2) {
  document.write("<p><strong>You earned a bronze crown.</strong></p>");  
} else {
  document.write("<p><strong>No crown for you. You need to study.</strong></p>");
}
```
