# Function Composition

`Function composition` -  is making new function out of other `functions` by combining the `logic` of other `functions`.

### Example

We got a `constant` named `"sentence"`.

```js
const sentence = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

We'd like to know how many words are in this sentence. Let's use `ramda` library to solve this. First we'll split a sentence into a list of words, which we can do by calling `ramda split() function`. 

```js
const sentence = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."

const wordList = R.split('', sentence)     //make a list of words
console.log(wordList)

//output:
//["Lorem", "ipsum", "dolor", "sit", "amet", "consectetur", "adipiscing", "elit", "sed", "do", "eiusmod", "tempor", "incididunt", "ut", "labore", "et", "dolore", "magna", "aliqua"]
```

Ramda also has a `length() function` which takes a `single parameter` for the thing we wanna get the length of.

```js
const sentence = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."

const wordList = R.split('', sentence)
console.log(wordList)

const wordCount = R.length(wordList)     //know the length of the word list
console.log(wordCount)

//output:
//["Lorem", "ipsum", "dolor", "sit", "amet", "consectetur", "adipiscing", "elit", "sed", "do", "eiusmod", "tempor", "incididunt", "ut", "labore", "et", "dolore", "magna", "aliqua"]
// 19
```
Well, we solved it in two steps and we had some `intermediate data`. The better way to solve the same proplem - using `functional composition`.
Ramda has a function called `compose`. This `compose function` allows you to combine two or more pure functions, and returns a new function that is a combination of those two functions.  Actually the uotput of the one function serves as the input for the another function. In our example let's put `split` function first in the `compose`, and here we won't pass any parameter to the `split funciton`. Because the `compose function` needs to be passed functions as parameters.

Now the output of the `split function` needs to be the input of the `length function`. 

```js

const countWords = R.compose(R.split)
```

The important fact about the `compose function` - it works from right to left! In other words the `last fucntion` we pass in the `compose function` is the first function called in the chain of function calles. 

![function-composition](../function-composition.png)

Knowing this fact we need to add `length() function` before the `split() function`. That's all we need to do to compose these two function together. 

```js

const countWords = R.compose(R.length, R.split)
```

What's returned from the `compose` is a new function, that we can call. This new function will require the parameters the last function requires, in our case the `split function`.

![split-function](../split-function.png)

Then the output of the `split function` is fed as the input for the `length function`. 

![split-lenght-function](../split-length-function.png)

The `value` of calling the `length function` is the `final return value` of the newly created `composed function`. 


![composed-function-value](../composed-function-value.png)

