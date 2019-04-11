# Create html element in React

We can create `html` element in React using `JSX` and `functions`. 

Two rules here: 
1. `listItem` recieves `raw data` (`array of objects`)
2. `listItem` returns a list of `html elements` (`<li></li>`)

```js
const [leads, setLeads] = useState([
    {name: "Ana", email: "example@hello.com", id: 1},
    {name: "Tom", email: "example@hello2.com", id: 2},
  ])

  const listItem = data => {
    const htmlList = data.map((lead)=>
    <li key={lead.id}>name: {lead.name}; email: {lead.email}; id: {lead.id} 
    <button onClick={() => deleteEntry(lead.id)}>Delete</button></li>
    )
  
    return htmlList
  }
```

We can just call `listItem function` in JSX `return()` with the `raw data` as an argument (`array` with `leads` in our case), and this function returns for us the `<li>` and `<button>` `html elements` with the needed `data`. 

```jsx
return(
<ol>{listItem(leads)}
</ol>
) 
```

You can use `JSX` inside of `if statements` and `for loops`, assign it to `variables`, accept it as `arguments`, and return it from `functions`:

1. return from a `function`; use inside `if statements`
```jsx
const user = {
  firstName: 'Harper',
  lastName: 'Perez'
}; 

function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

2. assign to a `variable`

```jsx
const element = <img src={user.avatarUrl} />;

const element2 = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);

const element3 = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);     //JSX tags may contain children

```