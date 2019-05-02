# The useState Hook with an object argument

What if we wanna two or more pieces of `state` on our component? 
The first strategy is to follow all of the old `class-based-component` paradigm of using a plain `js object` to store our `state`. And this works but with some caveats. 
Let's make this with a simple form. 

```jsx
import React, {useState} from 'react';

const App = () => {
  
  const [address, setAddress] = useState({
    city: '',
    country: '',
  })


return (
    <div>
      <h1>Welcome to the app</h1>
      <form>
        <div>
          <input type="text"
          placeholder="City"
          value={address.city}
          name="city" 
          />
        </div>

        <div>
          <input type="text"
          placeholder="Country"
          value={address.country}
          name="country" 
          />
        </div>
      </form>
      <div>
        You live in {`${address.city}, ${address.country}`}
      </div>
    </div>
  );
}

export default App;
```
Now we have our `simple form` but there is one more thing we need to setup - the `functions` which are gonna handle the changes of the `inputs` as the user types. 
So, we are going to declare two `functions` that are going to handle changes in our `input fields`. An `input field` has an `onChange` handler. 

```jsx
import React, {useState} from 'react';

const App = () => {
  
  const [address, setAddress] = useState({
    city: '',
    country: '',
  })

const handleCityChange = (event) =>{
  setAddress({
    ...address, city: event.target.value
  })
  }
  
const handleCountryChange = (event) => {
  setAddress({
   ...address, country: event.target.value
  })
  }

return (
    <div>
      <h1>Welcome to the app</h1>
      <form>
        <div>
          <input type="text"
          placeholder="City"
          value={address.city}
          name="city" 
          onChange={handleCountryChange}
          />
        </div>

        <div>
          <input type="text"
          placeholder="Country"
          value={address.country}
          name="country" 
          onChange={handleCountryChange}
          />
        </div>
      </form>
      <div>
        You live in {`${address.city}, ${address.country}`}
      </div>
    </div>
  );
}

export default App;
```
Here the Hook simply takes whatever you give to your `setter function` (setAddress in our case) and overwrites the `state value` with it. 