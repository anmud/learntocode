# Define a custom Hook (User Keypresses)

Here we'll take a look at how we can extract business logic bult on `hooks` to `functions` that are not `React components` or another words `functions` that do not render apart our `visual UI`. These are called `custom hooks` and represent a powerful paradigm, cos they allow to reuse business logic across multiple components, but only have defined once. 

The following `App` component actually has two responsibilities: 

- to keep track of what the `user` has typed and to add/remove `event listeners`
- to render `UI` 

##### App
```jsx
import React, {useState, useEffect, createContext, useContext} from 'react';


const App = () => {
  
const [userText, setUserText] = useState('')
  const handleUserKeyPress = event => {
    const {key, keyCode} = event
    if (keyCode === 32 || (keyCode >= 65 && keyCode <=90)) {
     setUserText(`${userText}${key}`)
    }
  }
  
  useEffect(()=>{
    window.addEventListener('keydown', handleUserKeyPress)
    return ()=>{
      window.removeEventListener('keydown', handleUserKeyPress)
    }
  })

  return (
    <div>
      <h1>Welcome to the app</h1>
      
      <div>
        <h1>Feel free to type. Your text will show up below!</h1>
        <blockquote>{userText}</blockquote>
      </div>

      
    </div>
  );
}

export default App;
```

Let's say we wanna bild a second `component` that has the exact same typing functionality but a diffetern `UI`. But we don't want to re-write or copy and paste all of the business logic to our second `component`. How can we extract this `user typing` functionality so it can be used in multiple components?

All we have to do is to define `hooks logic` in a js `function` that we can then invoke in the `component` where we wanna use that logic.
When we define a `custom hook` it should always start with the word "use", and then the name you want (useKeyPress in our case). And in this `function` we paste the code with hooks. 

##### App
```jsx
import React, {useState, useEffect, createContext, useContext} from 'react';


const App = () => {
  
  return (
    <div>
      <h1>Welcome to the app</h1>
      
      <div>
        <h1>Feel free to type. Your text will show up below!</h1>
        <blockquote>{userText}</blockquote>
      </div>

      
    </div>
  );
}

const  useKeyPress = () => {
    const [userText, setUserText] = useState('')
  const handleUserKeyPress = event => {
    const {key, keyCode} = event
    if (keyCode === 32 || (keyCode >= 65 && keyCode <=90)) {
     setUserText(`${userText}${key}`)
    }
  }
  
  useEffect(()=>{
    window.addEventListener('keydown', handleUserKeyPress)
    return ()=>{
      window.removeEventListener('keydown', handleUserKeyPress)
    }
  })
}

export default App;
```

`useKeyPress` is not a `react component`, we are not actually returning any `jsx`. The next step is to use `useKeyPress` wihin the body of `App`. But then we have a little problem - the `App` component is dependent on the `constant` "userText" which isn't available in scope, cos it hasn't been defined. So, we need somewhere of getting `userText` state variable outside of `userKeyPress` function. The simpliest way to do that is to return it in `userKeyPress` function. 


##### App
```jsx
import React, {useState, useEffect, createContext, useContext} from 'react';


const App = () => {
  useKeyPres()    //call here 

  return (
    <div>
      <h1>Welcome to the app</h1>
      
      <div>
        <h1>Feel free to type. Your text will show up below!</h1>
        <blockquote>{userText}</blockquote>
      </div>

      
    </div>
  );
}

 const useKeyPress = () => {
    const [userText, setUserText] = useState('')
  const handleUserKeyPress = event => {
    const {key, keyCode} = event
    if (keyCode === 32 || (keyCode >= 65 && keyCode <=90)) {
     setUserText(`${userText}${key}`)
    }
  }
  
 useEffect(()=>{
    window.addEventListener('keydown', handleUserKeyPress)
    return ()=>{
      window.removeEventListener('keydown', handleUserKeyPress)
    }
  })
  return userText
}

export default App;
```

We can return also multiple things, e.g `array` or `object`, if we wanna allow a `component` to use e.g `setUserText` function to update the `state variable`. We can also return it if e.g two different components have two different functionalities or two different pieces of logic that they determine => to update the `state` variable we can export `setUserText` function. 

So, because we returned our `userText` state variable, we can assign this to a `variable` within the body of our `App` component - `const userText = useKeyPress()`. 

##### App
```jsx
import React, {useState, useEffect, createContext, useContext} from 'react';


const App = () => {
 const userText = useKeyPres()    //call here 

  return (
    <div>
      <h1>Welcome to the app</h1>
      
      <div>
        <h1>Feel free to type. Your text will show up below!</h1>
        <blockquote>{userText}</blockquote>
      </div>

      
    </div>
  );
}

 const useKeyPress = () => {
    const [userText, setUserText] = useState('')
  const handleUserKeyPress = event => {
    const {key, keyCode} = event
    if (keyCode === 32 || (keyCode >= 65 && keyCode <=90)) {
     setUserText(`${userText}${key}`)
    }
  }
  
 useEffect(()=>{
    window.addEventListener('keydown', handleUserKeyPress)
    return ()=>{
      window.removeEventListener('keydown', handleUserKeyPress)
    }
  })
  return userText
}

export default App;
```

More important is the other benefit. Now `useKeyPress` is a `function` that is incredibly reusable. We can use it in another `component`, in any other `component` that wants to have this `functionality`, and all we have to do is invoke it. `useKeyPress` is a plain js `function`, we can customise it to work in a way that we want, by giving it smth. lik e `arguments`. 

Let's say we wanna invoke `useKeyPress`, but we also want some text already be typed down when ever the page first loads. We can customise our `useKeyPress` hook to take a parameter `"startingValue"`. Now instead of storing `default variable` of our `state variable` called "userText" as an `empty string`, we can view "startingValue". And when we go to the `component` which we wanna use this `custom hoook`, we'll give it a `custom value`. Now our `userText` variable is initialised with a `custom string value`.

##### App
```jsx
import React, {useState, useEffect, createContext, useContext} from 'react';


const App = () => {
 const userText = useKeyPres('Once upon a time...')    //custom value here

  return (
    <div>
      <h1>Welcome to the app</h1>
      
      <div>
        <h1>Feel free to type. Your text will show up below!</h1>
        <blockquote>{userText}</blockquote>
      </div>

      
    </div>
  );
}

 const useKeyPress = (starttingValue) => {
    const [userText, setUserText] = useState(startingValue)
  const handleUserKeyPress = event => {
    const {key, keyCode} = event
    if (keyCode === 32 || (keyCode >= 65 && keyCode <=90)) {
     setUserText(`${userText}${key}`)
    }
  }
  
 useEffect(()=>{
    window.addEventListener('keydown', handleUserKeyPress)
    return ()=>{
      window.removeEventListener('keydown', handleUserKeyPress)
    }
  })
  return userText
}

export default App;
```