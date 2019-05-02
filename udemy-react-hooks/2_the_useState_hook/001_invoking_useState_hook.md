# Invoking the useState Hook

A `hook` as we already know is a plain `js function` that hooks into, or connects to, or enables acces to a special React feature. 

`useState` is a hook that allows us to use the React feature of `state`, without making a `class-based` componenet. In fact hooks like `useState` cannot even be written inside the React classes; these hooks have to be envocked in the body of a `functional React component`.

`useState` expect one initial `argument` which is `state`, and this represents the starting value of this piece of `state`.  

```jsx
import React, {useState} from 'react';

const App = () => {
  useState(false)

  return (
    <div>
      <h1>Welcome to the app</h1>
      <button>My text</button>
    </div>
  );
}

export default App;
```
The `useState()` function actually returns us the `array` (`[]`) with two elements: the first element is the current value of `state`, and the second element is the `function` to update the `current value` of the `state`. 

**Important here:** we cannot hook a `conditional statement`. You cannot invoke `useState` anywhere except the main body of a `functional component`. 
The `useState` declares what is called the `state variable` - it's a `variable` that's going to store `state`, a `variable` that's going to remember `data`; magical part here is that React will remember the `current value` of the `state variable` whenever this `function` runs again - the `App() function`.  Whenever we re-render the `App` to the screen, the `entire` body of the `functional component` is gonna re-run, and rather than reuse the `state` with the value (false in our case), React is going to remember the `current value` when the `function` runs again. 