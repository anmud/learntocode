# while Loops

Awesome job! `for` loops are great, but they have a limitation: you have to know how many times you want the loop to run. What if you want a loop to execute an unknown or variable number of times instead?

For example, if we have a deck of cards and we want to flip cards (loop a card flipping function) until we get a Spade, how could we write that in JavaScript?

That's the purpose of the `while` loop. It looks similar to a `for` loop. See the example below.

```js
while (condition) {
  // Code block that loops until condition is false
}
```
The loop begins with the keyword while.
Inside the parentheses, we write a condition. As long as the condition evaluates to `true`, the block of code will loop.
Inside the code block, we can write any code we'd like to loop.

### Example

![while-loop](../while-loop.png)

The code `currentCard = cards[Math.floor(Math.random() * 4)];` will generate a random number between `0` and `3`, the range of indices of the cards array, and reassign `currentCard` to a new card from that array. Because the `while` loop only runs if the card is NOT a Spade, the value of `currentCard` will only be logged to the console if it is not `'Spade'`.
If we run the code a few times to see the output changing. You can see the `while` loop guessing a card, then seeing if it is a Spade, over and over, until it finds one.

