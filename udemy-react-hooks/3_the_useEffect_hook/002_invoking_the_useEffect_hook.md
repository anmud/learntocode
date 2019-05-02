# Invoking the useEffect Hook

Like `useState` this is a Hook that is available from the `React library` itself - `import React, {useState, useEffect} from 'react';`.

The `useEffect` hook accepts a `function`, a `callback function` as an `argument`. This `function` we call a `side effect`. What does it mean? Well, an effect is just a sequence of one or more steps, it's a procedure that we want the `component` to execute every time it renders or re-renders. 
The `useEffect` hook acts like a combination of the `componentDidMount`, `componentDidUpdate` and `componentWillUnmount` lifecycle methods. 


```jsx
import React, {useState, useEffect} from 'react';


const App = () => {
  
  const [count, setCount] = useState(0)
 
  const increaseCount = ({count, setCount}) => setCount(count + 1)
  const decreaseCount = ({count, setCount}) => setCount(count - 1)
  
  
useEffect(() => {
  console.log(`I am inside the useEffect function. The current count is ${count}`)
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
Every time our `component` renders or re-renders, the `function` or the `effect` that we pass to the `useEffect` hook, that `function` will be re-declared. And that is a good thing cos each time the `useeffect` hook runs this `function`, the `function` will have a new up-to-date present `current value` of the `count` state variable. 

So, let's see at what os going on here step by step: 

- Every single time we press the `button` we invoke the `click handler` (handleIncrease/handleDecrease in our case). What that is doing - is calling the `setCount` function, that we've got from our `useState` hook, ehich updates the `value` of a `count state variable`.
- Whenever the `value` of a `state variable` is updated we force a `component` re-render.
- Whenever the `component` re-renders the `useEffect` hook runs the `function` that we passed to it. 
