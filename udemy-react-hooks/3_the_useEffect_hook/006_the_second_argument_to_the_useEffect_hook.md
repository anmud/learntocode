# The second Argument to the useEffect Hook

Let's say in our `Counter app` we wanna our `count` to change color. First we need to add a third `button` that will change color of the `count`. 
For that we need to create a new `state variable` "color" and a `function` that's gonna check if the current color red, then we gonna change it to green and vice versa - and pass this `function` to our `equivalent setter function`. 

##### App
```jsx
import React, {useState, useEffect} from 'react';
import Counter from './Counter'


const App = () => {
  
  const [count, setCount] = useState(0)
  const [visible, setVisible] = useState(false)
  const [color, setColor] = useState('red')  //create color variable 

  const increaseCount = ({count, setCount}) => setCount(count + 1)
  const decreaseCount = ({count, setCount}) => setCount(count - 1)
  const resetCount = ({count, setCount}) => setCount(0)
  const handleColorChange = () => {                 //create handleChange function for the button
      const nextColor = (color === "red") ? "gold" : "red"
     return setColor(nextColor)
  }
  
  return (
    <div>
      
      <div>
      <button onClick={() => setVisible(!visible)}>
      
      Show / Hide the Counter Component
      
      </button>
      {visible && <Counter 
      count={count}
      setCount={setCount}
      increaseCount={increaseCount}
      decreaseCount={decreaseCount}
      resetCount={resetCount}
      color={color}
      setColor={setColor}
      handleColorChange={handleColorChange}
      />}
     </div>
     
      
    </div>
  );
}

export default App;
```

##### Counter
```jsx
import React, {useState, useEffect} from 'react';


const Counter = (props) => {
 

useEffect(() => {
  console.log(`I am inside the useEffect function. I will only run upon mounting. The current count is ${props.count}`)

  return () => {
    console.log('I am removing anything that was setup above. But now I will only run when component is being unmounted.')
  }
}, [props.count])  // add second argument here 

  return (
    <div>
     
      <h1 style={{color: props.color}}>{props.count}</h1>
      <button onClick={()=>props.increaseCount({count: props.count, setCount: props.setCount}) }>Increase</button>
      <button onClick={() =>props.decreaseCount({count: props.count, setCount: props.setCount})}>Decrease</button>
      <button onClick={() =>props.resetCount({count: props.count, setCount: props.setCount})}>Reset</button>

      <br/>

      <button onClick={() => props.handleColorChange({color: props.color, setColor: props.setColor})}>Change color</button>
      
    </div>
  );
}

export default Counter;
```


Well,  what we really want to do here is to have our `side effect` run only when a specific piece of `state` changes  - and that is exactly what `second argument` to `useEffect` represents. It represents what exactly pieces of `state` you want React to keep track of. It's the `values` that we pass to that `array` that React is going to monitor, it's only when those `values` change React is going to force the `function` that we pass to `useEffect` to run. 

```js
useEffect(() => {
  console.log(`I am inside the useEffect function. I will only run upon mounting. The current count is ${props.count}`)

  return () => {
    console.log('I am removing anything that was setup above. But now I will only run when component is being unmounted.')
  }
}, [props.count])  // add second argument
```
We say to React: "Only run `useEffect`, the callback function that we passed in, whenever the `value` of the `count state variable` changes".  And now whenever the `color` of the `count` changes the `useEffect` is not going to run. 

Well, we onlu wanna pass an `array` as a second `argument` when we want to customise which `state variables` we want to keep track of. As well as an empty `array` works here in order to prevent any `state changes` or any `render changes` from triggering the `useEffect` to run. We are telling here: "Regardless of what `state variables` we have, we don't want to keep track of any `state variable`. So, any `state changes` in our `Counter component` will not trigger `useEffect` to run again". That's why an `empty array` works. 