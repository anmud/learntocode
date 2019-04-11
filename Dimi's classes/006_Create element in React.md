# Create html element in React

We can create `html` element in React using `JSX` and `functions`. 

Two rules here: 
1. listItem recieves raw data (array of objects)
2. listItems returns a list of html elements (<li></li>)

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
    console.log(htmlList)
    return htmlList
  }
```

We can just call `listItem function` in JSX `rerurn()`. 

```jsx
return(
<ol>{listItem(leads)}
   </ol>
) 
```