# Cleaning Up by Returning a Function from the Effect 1

Let's take look how we can clean up some of the setup code that we put in the `useEffect` function, by returning a `function` from the `useEffect` function. 

The `useEffect` hook comes equiped with a very cool feature, if we are performing some kind of setup in the `effect function`, what we can do is return a `function` from inside that `effect function`. And the `function` that we return can specify the tear down logic. In other words the logic that we write inside the `returned function` can tell React how to break everything down. 

This is designed to emulate the behaviour of two `lifecycle methods` from `class-based` components: namely `componentDidMount` and `componentDidUpdate`. 

```jsx
import React, {useState, useEffect} from 'react';


const App = () => {
  
  const [count, setCount] = useState(0)
 
  const increaseCount = ({count, setCount}) => setCount(count + 1)
  const decreaseCount = ({count, setCount}) => setCount(count - 1)
  
  
useEffect(() => {
  console.log(`I am inside the useEffect function. The current count is ${count}`)

  return () => {
     console.log('I am removing anything that was setup above')
  }
})

  
  return (
    <div>
      <h1>Welcome to the app</h1>
      
      <h1>{count}</h1>
      <button onClick={()=>increaseCount({count: count, setCount: setCount}) }>Increase</button>
      <button onClick={() =>decreaseCount({count: count, setCount: setCount})}>Decrease</button>
     
    </div>
  );
}

export default App;
```
In this `return function` we specify the tear down process. The next time `useEffect` runs this is what we want to run first, that's going to tear down the previous run-through of `useEffect`. 
