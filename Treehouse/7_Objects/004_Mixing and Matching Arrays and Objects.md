# Mixing and Matching Arrays and Objects

It's very common to combine `arrays` and `objects` by making an `array of objects`. Objects let you use clear names to identify your data. 

### Example of the quizz game with the `array of objects`

```js
var questions = [
  { question: 'How many states are in the United States?', 
    answer: 50
  },
  { question: 'How many continents are there?',
    answer: 7
  },
  {question: 'How many legs does an insect have?', 
    answer: 6]
  }
];

var correctAnswers = 0;
var question;
var answer;
var response;

function print(message) {
  document.write(message);
}

for (var i = 0; i < questions.length; i += 1) {
  question = questions[i].question; //we access property values
  answer = questions[i].answer; //we access property values
  response = prompt(question);
  response = parseInt(response);
  if (response === answer) {
    correctAnswers += 1;
  } 
}

html = "You got " + correctAnswers + " question(s) right."
print(html);
```
We can write our `array` more compact:

```js
var questions = [
    {question: 'How many states are in the United States?', answer: 50},
    {question: 'How many continents are there?', answer: 7},
    {question: 'How many legs does an insect have?', answer: 6}
];
```

