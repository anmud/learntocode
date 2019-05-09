# Invoking the useContext Hook

So, to refactor the code with `Context` hook, we'll need also `useContext` hook from the React library. 

Then we create our `Context object` with invoking `createContext()` function; this is usually done in a separate file, but for the example here we'll have this in the `App` file. 
And let's create `functional components`. 

##### App
```jsx
import React, {useState, createContext, useContext} from 'react';
import Child from './Child'

export const NameContext = createContext()

const App = () => {
  
  const [name, setName] = useState({
    name: "Billy Shakespere",
})


  return (
    <div>

      <NameContext.Provider value={name}>
          <Child/> 
      </NameContext.Provider>

    </div>
  );
}

export default App;
```

##### Child
```jsx
import React from 'react';
import Grandchild from './Grandchild'


const Child = () => {

  return (
    <div>
     
     <section className="child">
     <Grandchild/>
     </section>
      
    </div>
  );
}

export default Child;
```

##### Grandchild

```jsx
import React  from 'react';
import Button from './Button'


const Grandchild = () => {
 
  return (
    <div className="grandchild">
     
     <Button/>
      
    </div>
  );
}

export default Grandchild;
```

##### Button
```jsx
import React, {useContext} from 'react';
import {NameContext} from './App'


const Button = (props) => {
 const name = useContext(NameContext)
  return (
    <div>
    
    <button>{name.name}</button>
      
    </div>
  );
}

export default Button;
```