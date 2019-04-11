# SetState Notes

Let's look at the `addName` function step by step. We wanna change `inputState`, for that we need to use `setInput` function that serves to change the `state` (- `inputState` in our example).

```js
const [inputState, setInput] = useState({name:"", city: "", countryCode:""})


  const addName = (event) =>{
    console.log(event.target.value)
    setInput({...inputState, name: event.target.value} )
  }
```


1.  `setInput({})` -> we call `setInput` function and first we create a new `object` using `{}`
2.  `setInput({...inputState})` -> then we spread the `properties` from `inputState object` (namely: `{name:"", city: "", countryCode:""}`) into a new object - like we create the copy of the `object`.
Each time when we `spread` an `object`, a `new object` gets created (a copy). We don't overwrite the `original object`.

3. `setInput({...inputState, name: event.target.value})` -> and finally we overwrite the `"name"` property of the newly created object with the `value` from the `input`. 
