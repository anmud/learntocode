# Call Stack

`Call Stack` is a special data structure - a way of storing information, data that allows us to track whare we are currently, whare is the thread of execution currenlty in our code. 

We start from our `global execution context`. `Call Stack` is the data sructure of the format when - the last thing you put into it is the first thing you take out of it. 

**We keep track of the functions being called in JavaScript with a Call stack**

Tracks which execution context we are in - that is, what `function` is currently being run and where to return to after an `execution context` is popped off the stack.

One `global execution context`, multiple `function contexts`

