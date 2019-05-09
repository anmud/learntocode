# Another useEffect example: User Input 

Let's build an `app` where a `user` can type any `lower case letter` or a `space` with the `key board` and we wanna take all te `letters` that the `user` has typed so far and putput them to the screen. 
So, as the `user` adds the `characters` we gonna see them on the screen. 

In order to accomplish this we need to add an ` event listner` in the `useEffect` hook and we also wanna make sure that we removed the previuos `event listner` before the `function` runs again. 

So, we know that we need a `state` variable to store everything that the `user` has typed.

```jsx
import React, {useState, useEffect} from 'react';

const App = () => {
  
const [userText, setUserText] = useState('')
  


return (
    <div>
    
        <h1>Feel free to type. Your text will show up below!</h1>
        <blockquote>{userText}</blockquote>
      
    </div>
  );
}

export default App;
```

In order for `browser` to automatically update our `userText` state variable we need to setup an `eventListner`. We can do that within a `function` (of effect) that we pass in our `useEffect` hook. 

```jsx
import React, {useState, useEffect} from 'react';

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
    
        <h1>Feel free to type. Your text will show up below!</h1>
        <blockquote>{userText}</blockquote>
      
    </div>
  );
}

export default App;
```

`useEffect` will take an `anonimous function` and inside this `function` we gonna have `addEventListener`. This `method` gonna have two `parameters`: the first is a string that represents what `event` you want the `browser` to listen to (in our case - a keydown event); the second parameter - what `function`/effect you wanna execute whenever a `keydown ` effect occurs.
So, whenever the `component` renders or re-renders we wanna make sure that we add an `eventListener` to our `window`, that tells the `browswer` whenever the `user` presses any `key` down we wanna invoke `handleUserKeyPress`. 

`handleUserKeyPress()` - whenever the `browser` invokes this `function`, it's automatically gonna pass in an `event object`. If we wanna keep track of what the `user` typed, the actual character, we can get from the `event object` the `property` called **`key`**, and also since our task is to limit this to simply spaces and lower case letters, we also gonne distructure here the `property` called **`keyCode`**. 

Then we'll use a basic `conditional` that is going to limit us to keydowns as space bars as well as lower case characters. 

```js
if (keyCode === 32 || (keyCode >= 65 && keyCode <=90)) {
     setUserText(`${userText}${key}`)
    }
```

And we surely need the `tear down` part, because if we forget to erase everything that we've built up we gonna continue stucking all the work and this can be particulary dangerous if this `component` removed from the screen, however all `event listeners` still persist on the `window` object and we still are keeping track of this and trying to do smth. with a `component` that is no longer `mounted`. So, we have to remember to tear down everything that we set up. 

And the way we tear down is very simple, we just return the `function` and the only we need to do from within from this `function` is to remove `event listener`. 