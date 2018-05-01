# Event Bubblind and Delegation

An `event` received by an `element` doesn't stop with that one `element`. That `event` moves to other `elements` like the `parent`, and other `ancestors` of the element. This is called `"event bubbling"`.

Since the handlers are not bound to individual list `items`, any item can be added after the `listener` has run, and no additional setup is required for that item's events to be handeled. When we are trying to decide which element to use **remember** it has to be an ancestor of the target elements. 

In our example let's add it to the `div` which contains the whole `list`

**HTML**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>JavaScript and the DOM</title>
    <link rel="stylesheet" href="css/style.css">
  </head>
  <body>
    <h1 id="myHeading">JavaScript and the DOM</h1>
    <p>Making a web page interactive</p> 
    <button id="toggleList">Hide list</button>
      <div class="list">
      <p class="description">Things that are purple:</p>
      <input type="text" class="description"> 
      <button class="description">Change list description</button>
      <ul>
        <li>grapes</li>
        <li>amethyst</li>
        <li>lavender</li>
        <li>plums</li>
      </ul>
        <input type="text" class="addItemInput"> 
      <button class="addItemButton">Add Item</button>
        <button class="removeItemButton">Remove last item</button>
        </div>
    <script src="app.js"></script>
   
  </body>
</html>
```
We need to place each `eventListner` to `listDiv`.

```js
const toggleList = document.getElementById('toggleList');
const listDiv = document.querySelector('.list');
const input = document.querySelector('input');
const p = document.querySelector('p.description');
const button = document.querySelector('button');
const addItemInput = document.querySelector('input.addItemInput');
const addItemButton = document.querySelector('button.addItemButton');
const removeItemButton = document.querySelector('button.removeItemButton');


listDiv.addEventListener('mouseover', () =>{               //place listeners to listDiv
listItems[i].textContent = listItems[i].textContent.toUpperCase();
});

listDiv.addEventListener('mouseout', () =>{
listItems[i].textContent = listItems[i].textContent.toLowerCase(); 
});


toggleList.addEventListener('click', () =>{
if(listDiv.style.display == 'none'){
  toggleList.textContent = 'Hide list';
  listDiv.style.display = 'block';
}else{
  toggleList.textContent = 'Show list';
listDiv.style.display = 'none';
}
});

button.addEventListener( 'click', () => {
 p.innerHTML = input.value + ':';                      
});

addItemButton.addEventListener('click', () =>{
let ul = document.getElementsByTagName('ul')[0];                               
let li = document.createElement('li'); 
li.textContent = addItemInput.value;
ul.appendChild(li);
});

removeItemButton.addEventListener('click', () =>{
let ul = document.getElementsByTagName('ul')[0];                               
let li = document.querySelector('li:last-child'); 
ul.removeChild(li);
});
```

**BUT** looking back inside these `call back functions` there is a problem, when `events` fire on `listDiv` how do we know which `list item` is true to the `event`?

Look for the solution in 021_The Event Object lesson. 
