# Limiting useEffect to Mounting and Unmounting

What if you only want the `useEffect` function to run when the `component` first appears and right before it disappears? What if you want any re-renders, e.g if the `state` changes or the `props` change and `Counter component` re-renders, what if you want that re-render NOT to trigger `useEffect` to run?

Real-life use-case that can be a good example:
Imagine making smth. like a simple `API request`, the `component` loads and we wanna get some information from the `backend`. 

If we put this logic inside the `useEffect` to make the `API request`, then every single time the `state` and `props` change and the `component` re-rendres and the `useEffect` hook runs again, then every single time we gonna be running this logic, and every single time we gonna be making this `API request` for the very same `data` - and that's surely inefficient. 

What we'll do here we'll setup an initial `API request`, but also make sure that the `component` knows that it's just for the one tome use, and that it shouldn't make this request again. It should only make it when the `component` mounts for the first time and/or unmounts. 

How can we setup smth. like that? The solution is to pass an `empty array` as the `second argument` to the `useEffect` hook. 


##### Counter 
```jsx
import React, {useState, useEffect} from 'react';


const Counter = (props) => {
 

useEffect(() => {
  console.log(`I am inside the useEffect function. I will only run upon mounting. The current count is ${props.count}`)

  return () => {
    console.log('I am removing anything that was setup above. But now I will only run when component is being unmounted.')
  }
}, []) //array as a second argument

  return (
    <div>
     
      <h1>{props.count}</h1>
      <button onClick={()=>props.increaseCount({count: props.count, setCount: props.setCount}) }>Increase</button>
      <button onClick={() =>props.decreaseCount({count: props.count, setCount: props.setCount})}>Decrease</button>
      <button onClick={() =>props.resetCount({count: props.count, setCount: props.setCount})}>Reset</button>
      
    </div>
  );
}

export default Counter;
```

From this point, whenever our `component` re-renders, e.g. when we click `increase` or `decrease` buttons and the `state` changes, the `visual UI` changes cos the `component` re-renders , at this point `useEffect` hook will not run again. 
It means that `useEffect` is not running its effect (callback function), it also means that our `tear-down function` that we returned at the first time when the `component` was first mounted, is still being held in memory, React is still keeping track of this, but it's not actually executing it. 
And the only time when this `tear-down` function is executed - is whenever we complete the `tear-down` with unmounting, when `useEffect` runs for the last time.  


