# Challenge: Reusing Custom Hooks in Multiple Componnets 

In this challenge we are going to build out a `user form` with three separate `input fields`. But we wanna move all of the logic of keeping track of each `input` and its `value` to a separate `useInput` custom hook. We'll start with a simple `App` with the `user form inside` which contains three inputs for the `user`. And let's define the basic `custom hook` "useINput". 

#### App
```jsx
import React from 'react';
import Form from './Form'

const useInput = () => {

}

const App = () => {
  return (
    <div>
     
     <Form useInput={useInput}/>

    </div>
  );
}

export default App;
```

#### Form
```jsx
import React  from 'react';

const Form = (props) => {

return (
    <div>

 <form>

   <input 
   type="text"
   placeholder="Name"
   value={}
   onChange={}
   />

<input 
   type="text"
   placeholder="Surname"
   value={}
   onChange={(}
   />

<input 
   type="number"
   placeholder="Age"
   value={}
   onChange={(}
   />
  
 </form>


    </div>
  );
}

export default Form;
```

The challenge: 

- fill out `useInput` 
- invoke it in the `App component` 
- make all of this functional 
- return some values from `useInput` hook and use them within the `value` and `onChange` properties
- `useInput` hook is going to return probably some `data structure` that's going to allow us to store multiple `properties`, and they all have the same name 

#### App

```jsx
import React, {useState} from 'react';
import Form from './Form'

const useInput = () => {
  const [inputValue, setInput] = useState('')

  const onChange = (event) => {
    return setInput(event.target.value)
  }

  return {
    inputValue,
    onChange,
  }
}

const App = () => {


  return (
    <div>
     
     <Form useInput={useInput}/>


    </div>
  );
}

export default App;
```

#### Form 
```jsx
import React  from 'react';

const Form = (props) => {

const {inputValue: name, onChange: handleNameChange} = props.useInput()
const {inputValue: surname, onChange: handleSurnameChange} = props.useInput()
const {inputValue: age, onChange: handleAgeChange} = props.useInput()

return (
    <div>
     

 <form>

   <input 
   type="text"
   placeholder="Name"
   value={name}
   onChange={(event) => handleNameChange(event)}
   />

<input 
   type="text"
   placeholder="Surname"
   value={surname}
   onChange={(event) => handleSurnameChange(event)}
   />

<input 
   type="number"
   placeholder="Age"
   value={age}
   onChange={(event) => handleAgeChange(event)}
   />
  
 </form>
</div>
  );
}

export default Form;
```

### Version-2 

There is also a more elegant way to use `useInput` hook. The more elegant way is to get rid of all of `inputValue` and `onChange` properties in `useInput()` all together. Cos the `value` and `onChange` attributet on the `input` - working the exact same way; we need to display a `value` which is always gonna be what is the `value` of our `value state variable`, and we always need to pass in a `function` that's going to update that `value`, which again - `onChange` functionality inside the hook remains exact same. 
So, in our `input` element we can get rid of `value` and `onChange` properties and destructure the `object` that we get back from invoking our `useInput hook`. 

```jsx
<input 
   type="text"
   placeholder="Name"
   {...useInput()}
   />
```
We are invoking `useInput` hook, we know that this `hook` is going to return an `object` with two `properties`, and those `properties` are always going to be: `value` and `onChange`. What we can do is to take this `object` that we get back as the returned `value` of `useInput()` function invocation, and destructure these two `properties` to serve as our `attributes` to our `input field`. 
Each `state` variable stays independent. 


#### Form 
```jsx
import React  from 'react';

const Form = (props) => {


return (
    <div>
     

 <form>

   <input 
   type="text"
   placeholder="Name"
   {...props.useInput()}
   />

<input 
   type="text"
   placeholder="Surname"
    {...props.useInput()}
   />

<input 
   type="number"
   placeholder="Age"
    {...props.useInput()}
   />
  
 </form>
</div>
  );
}

export default Form;
```

#### App

```jsx
import React, {useState} from 'react';
import Form from './Form'

const useInput = () => {
  const [inputValue, setInput] = useState('')

  const onChange = (event) => {
    return setInput(event.target.value)
  }

  return {
    inputValue,
    onChange,
  }
}

const App = () => {


  return (
    <div>
     
     <Form useInput={useInput}/>


    </div>
  );
}

export default App;
```