# Cleaning Up by Returning a Function from the Effect 2

There is one more `lifecycle method` that `useEffect` is designed to replace  - `componentWillUnmount`. 

Let's take a look at how it works. To simulate the process of unmounting let's make two components: `Counter` and `App`, and render `Counter` component conditionally - we just gonna simulate the process of mounting and unmounting. 

##### Counter
```jsx
import React, {useState, useEffect} from 'react';

const Counter = () => {
  
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

export default Counter;
```

##### App
```jsx
import React, {useState, useEffect} from 'react';

const App = () => {

const [visible, setVisible] = useState(false)
  
  
  return (
    <div>
      <button onClick={() => setVisible(!visible)}>Show / Hide the Counter Component</button>
      {visible && <Counter/>}
    </div>
  );
}

export default App;
```

- first we don't see our `counter component` on the screen, as well as the `useEffect` hook doesn't run yet, and it doesn't run yet  because the ` Counter component` is not yet on the DOM hasn't been mounted yet.
- the time when it's gonna mount is when we press `show/hide the Counter component` button. We are going to set the value of the `state "visible" variable` to `true` and that's gonna show the `Counter component` for the first time. 
- as soon as we press the button, that `useEffect` function runs for the first time  - this is the equivalent to `componentDidMount` - and inside this function we return another which is queued up and works as the equivalent of the `componentDidUpdate`. 
- when we click the `button` again to hide the `component` the only thing that runs is the `function` that was queued inside of `useEffect`. And since the `component` is leaving the DOM, the `function` makes sure that everything is back to original variant. 

