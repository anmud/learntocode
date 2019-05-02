# Using useState to build the counter 

First we invoke the `useState` and give it the `initial value` (`0`). And as well we need a `function` to handle button click. 

```jsx
import React, {useState} from 'react';

const App = () => {
  const [count, setCount] = useState(0)
  const increaseCount = ({count, setCount}) => setCount(count + 1)

  return (
    <div>
      
      <h1>{count}</h1>
      <button onClick={()=>increaseCount({count: count, setCount: setCount}) }>Increase</button>
    </div>
  );
}

export default App;
```

### Some more elements to the counter 

```js
import React, {useState} from 'react';


const App = () => {
  const [activated, setActivated]= useState(false)
  const [count, setCount] = useState(0)
  const buttonText = activated ? "Active" : "Inactive"
  const onClick = () => setActivated(!activated)
  const increaseCount = ({count, setCount}) => setCount(count + 1)
  const decreaseCount = ({count, setCount}) => setCount(count - 1)
  const resetCount = ({count, setCount}) => setCount(0)
  

  

  return (
    <div>
      <h1>Welcome to the app</h1>
      
      <h1>{count}</h1>
      <button onClick={()=>increaseCount({count: count, setCount: setCount}) }>Increase</button>
      <button onClick={() =>decreaseCount({count: count, setCount: setCount})}>Decrease</button>
      <button onClick={() =>resetCount({count: count, setCount: setCount})}>Reset</button>
    </div>
  );
}

export default App;
```