# Computed properies

`Computed properties` is used when we wanna to use a `variable value` as a `propery name`.

We can use `square brackets` in an `object` literal. That’s called `computed properties`.

For instance:

```js
let fruit = "apple";

let bag = {
  [fruit]: 5, // the name of the property is taken from the variable fruit
};

alert( bag.apple ); // 5 if fruit="apple"
```

The meaning of a `computed property` is simple: `[fruit]` means that the `property name` should be taken from `fruit` variable.

So, if a visitor enters "apple", `bag` will become `{apple: 5}`.

1. 

```js
const myFruit = "fruit"

const iEat = {[myFruit]: 'apple', vegetable: 'carrot'}

console.log(iEat)
//result - {fruit: "apple", vegetable: "carrot"}
```

2. 
```js
const name = "newProperty"

const obj = {name: "Dimitri", value: 10 }

const f = obj => {
  					// here the property name gets reassigned
  return {...obj, name: "Michael"}
}


const f_ = obj => {
  					// this is called computed property
  					// here the value of property name gets calculated and reassigned
  return {...obj, [name]: "Bob"}
}

console.log(
  f(obj),
 f_(obj)
 )
 // result 
 // {name: "Michael", value: 10}
 // {name: "Dimitri", value: 10, newProperty: "Bob"}
```
### More complex examle

Let's say we have a `form` where a user can change some `user data`. 

```jsx
 return (
    <form
      onSubmit={event => {
        event.preventDefault()

        props.updateUser(user.id, user)
      }}
    >
      <label>Name</label>
      <input type="text" name="name" value={user.name} onChange={handleInputChange} />

      <label>Username</label>
      <input type="text" name="username" value={user.username} onChange={handleInputChange} />

      <button>Update user</button>

    </form>
  )
```

Here on the html `<input>` element we have `attributes`: 

1. `"name"` - that holds some value, in our case - name/label of the `<input>` element. 

Like - `const name = 'name'` (variable "name" has a value name) 

and `const name = 'username'` (variable "name" has a value username) - here can be any `value`.

```jsx
const name = "name" // the label of the first input as a value
const name = "username" // the label of the second input as a value
```
2. `"value"` - that holds some `data` that a user enters in the `input.`

In other words we have an `object` -  where the attributes `"name"` and `"value"` are the `keys` that will hold some `value`.

```jsx
const inputObject = {
    name: "label of the input", 
    value: "data that a user enters in the input",
```

In case we want somehow to change the `data` that a user enters in the `input` we will use `onChange` event handler, which gets the `event object` as an argument.

```jsx
const [user, setUser] = useState(props.currentUser)

const handleInputChange = event => {
    const { name, value } = event.target
                        // [name] computed property
    setUser({ ...user, [name]: value })
  }
```

1. As the first step in the `handleInputChange` function we destructure the `event.target` object, which we get from the `event`. This `event.target` object has {name, value} keys. These `keys` already have some `values`, which we got with the `event object` when `event` on the `input` happened. 

`key "name"` as a value has the label of the exact `input field` which a user used, `key "value"` as a value has the `data` that a user entered in this exact `input field`. 

2. Then inside we call `setUser()` function, where we update the `user object` with the new values in `"name propery"`. And here we use `"name"` as a `computed propery`. 

Namely we use the `value` of the `key "name"` as a `property name` of the `user object` when we update it. 

```jsx
 const [users, setUsers] = useState([
  { id: 1, name: 'Tania', username: 'floppydiskette' },
  { id: 2, name: 'Craig', username: 'siliconeidolon' },
  { id: 3, name: 'Ben', username: 'benisphere' },
])
```

### Final code

```jsx
import React, { useState} from 'react'

const EditUserForm = props => {
  
 const [users, setUsers] = useState([
  { id: 1, name: 'Tania', username: 'floppydiskette' },
  { id: 2, name: 'Craig', username: 'siliconeidolon' },
  { id: 3, name: 'Ben', username: 'benisphere' },
])

const handleInputChange = event => {
    const { name, value } = event.target
    setUser({ ...user, [name]: value })
  }

  return (
    <form>
      <label>Name</label>
      <input type="text" name="name" value={user.name} onChange={handleInputChange} />

      <label>Username</label>
      <input type="text" name="username" value={user.username} onChange={handleInputChange} />

      <button>Update user</button>
    </form>
  )
}

export default EditUserForm
```