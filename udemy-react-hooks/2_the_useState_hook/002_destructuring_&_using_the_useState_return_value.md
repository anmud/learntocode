# Destructuring & using the useState Return value

Well, as we know the `useState()` hook returns an `array`, we can use ES6 `array destructuring` syntax to assign each of the two elements of the returned `array` to a separate `constant`. 

```jsx
import React, {useState} from 'react';


const App = () => {
  const [activated, setActivated] = useState(false)    //we destructure the array here 
  const buttonText = activated ? "Active" : "Inactive"

  return (
    <div>
      <h1>Welcome to the app</h1>
      <button>{buttonText}</button>
    </div>
  );
}

export default App;
```
To change the `state` we need a `click handler` where we'll call `setActivated()` function to change our `state`. What do we want the `activated` to be next? We want actually `activated` to be the opposite of what it is currently - namely `!activated`. So, when the `button` is clicked React is going to run the `function` and the `function` is going to run `setActivated function` which is going to update the value of the `state`.  This is the one way we can do it - with the `arrow function`.

```jsx
import React, {useState} from 'react';


const App = () => {
  const [activated, setActivated]= useState(false)
  const buttonText = activated ? "Active" : "Inactive"

  return (
    <div>
      <h1>Welcome to the app</h1>
      <button onClick={() => setActivated(!activated)}>{buttonText}</button>
    </div>
  );
}

export default App;
```

The other way to do this - we can take this `function` and extract it in a separate `function` right in the body of our `App component`.  

``jsx
import React, {useState} from 'react';


const App = () => {
  const [activated, setActivated]= useState(false)
  const buttonText = activated ? "Active" : "Inactive"
  const onClick = () => setActivated(!activated)

  return (
    <div>
      <h1>Welcome to the app</h1>
      <button onClick={onClick}>{buttonText}</button>
    </div>
  );
}

export default App;
```