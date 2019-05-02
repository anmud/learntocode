# Working with Multiple Pieces of State in a Hook-based Components

There is a more elegant way to work with multiple pieces of `state`. And that is when we invoke the `useState` Hook multiple times. We are free to use any `React Hook` as many times as we like in the body of the `functional component`. Let's call our `useState` twice.

```jsx
import React, {useState} from 'react';


const App = () => {

const [city, setCity] = useState('')
const [country, setCountry] = useState('')

const handleCityChange = (event) =>{
  setCity(event.target.value)
  }
  
const handleCountryChange = (event) => {
  setCountry(event.target.value)
  }
  

  return (
    <div>
      <h1>Welcome to the app</h1>
     
      <form>
        <div>
          <input type="text"
          placeholder="City"
          value={city}  //here we can get just city
          name="city" 
          onChange={handleCityChange}
          />
        </div>

        <div>
          <input type="text"
          placeholder="Country"
          value={country}  //here we can get just country
          name="country" 
          onChange={handleCountryChange}
          />
        </div>
      </form>
      <div>
         You live in {`${city}, ${country}`}   
      </div>
      <br/>
    </div>
  );
}

export default App;
```