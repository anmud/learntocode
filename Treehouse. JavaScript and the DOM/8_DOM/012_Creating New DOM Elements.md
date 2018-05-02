# Creating New DOM Elements


[MDN page for createElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)

You can create a new `element` in JS, using `document.createElement()` and passing in the `name` of the html `element` ('as a string') you want to create. 

### Example
Let's change our app to allow users to create new `items` to the `list`. 
First we need to add a new `text input` and a `button` in html file. We need also to change their `classes` and `textContent`. 

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
        <input type="text" class="addItemInput">  <!-- additional input -->
        <button class="addItemButton">Add Item</button> <!-- additional button -->
        </div>
    <script src="app.js"></script>
  </body>
</html>
```
Now in js file let's select our new elements.

```js
const toggleList = document.getElementById('toggleList');
const listDiv = document.querySelector('.list');
const input = document.querySelector('input');
const p = document.querySelector('p.description');
const button = document.querySelector('button');
const addItemInput = document.querySelector('input.addItemInput'); //select input
const addItemButton = document.querySelector('button.addItemButton'); //select button

toggleList.addEventListener('click', () =>{
if(listDiv.style.display == 'none'){
  toggleList.textContent = 'Hide list';
  listDiv.style.display = 'block';
}else{
  toggleList.textContent = 'Show list';
listDiv.style.display = 'none';
}
})
button.addEventListener( 'click', () => {
 p.innerHTML = input.value + ':';                      
});
```
Now we can add click `event listener` to a `button`.

```js
const toggleList = document.getElementById('toggleList');
const listDiv = document.querySelector('.list');
const input = document.querySelector('input');
const p = document.querySelector('p.description');
const button = document.querySelector('button');
const addItemInput = document.querySelector('input.addItemInput');
const addItemButton = document.querySelector('button.addItemButton');

toggleList.addEventListener('click', () =>{
if(listDiv.style.display == 'none'){
  toggleList.textContent = 'Hide list';
  listDiv.style.display = 'block';
}else{
  toggleList.textContent = 'Show list';
listDiv.style.display = 'none';
}
})
button.addEventListener( 'click', () => {
 p.innerHTML = input.value + ':';                      
});

addItemButton.addEventListener('click', () =>{   //listen to event
let li = document.createElement('li');           //create new item                  
});
```
Once the `item` is created, we can set the `text` we want it to contain.

```js
const toggleList = document.getElementById('toggleList');
const listDiv = document.querySelector('.list');
const descriptionInput = document.querySelector('input'); //changed input to descriptionInput
const descriptionP = document.querySelector('p.description');  //changed p to descriptionP
const descriptionButton = document.querySelector('button');  //changed button to descriptionButton
const addItemInput = document.querySelector('input.addItemInput');
const addItemButton = document.querySelector('button.addItemButton');

toggleList.addEventListener('click', () =>{
if(listDiv.style.display == 'none'){
  toggleList.textContent = 'Hide list';
  listDiv.style.display = 'block';
}else{
  toggleList.textContent = 'Show list';
listDiv.style.display = 'none';
}
})
descriptionButton.addEventListener( 'click', () => {  //changed button to descriptionButton
 descriptionP.innerHTML = descriptionInput.value + ':'; //changed p to descriptionP; changed input to descriptionInput
});

addItemButton.addEventListener('click', () =>{
let li = document.createElement('li'); 
li.textContent = addItemInput.value; //set the text here
});
```


