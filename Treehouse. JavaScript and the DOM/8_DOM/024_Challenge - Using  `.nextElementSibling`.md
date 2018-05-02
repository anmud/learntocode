# Challenge - Using `.nextElementSibling`
Here is [MDN page for nextElementSibling](https://developer.mozilla.org/en-US/docs/Web/API/NonDocumentTypeChildNode/nextElementSibling)

We need to implement a `down` button, which moves the item down. 

First we add `button` with a class `down` in html file.

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
        <li>grapes 
           <button class="up">Up</button>
          <button class="down">Down</button> <!-- add down button here -->
          <button class="remove">Remove</button>
        </li>
        <li>amethyst
           <button class="up">Up</button>
           <button class="down">Down</button> <!-- add down button here -->
          <button class="remove">Remove</button>
        </li>
        <li>lavender
           <button class="up">Up</button>
           <button class="down">Down</button> <!-- add down button here -->
          <button class="remove">Remove</button>
        </li>
        <li>plums
           <button class="up">Up</button>
           <button class="down">Down</button> <!-- add down button here -->
          <button class="remove">Remove</button>
        </li>
      </ul>
        <input type="text" class="addItemInput"> 
      <button class="addItemButton">Add Item</button>
        </div>
    <script src="app.js"></script>
   
  </body>
</html>
```
**JS**
```js
const toggleList = document.getElementById('toggleList');
const listDiv = document.querySelector('.list');
const input = document.querySelector('input');
const p = document.querySelector('p.description');
const button = document.querySelector('button');
const listUl = listDiv.querySelector('ul');
const addItemInput = document.querySelector('input.addItemInput');
const addItemButton = document.querySelector('button.addItemButton');
const removeItemButton = document.querySelector('button.removeItemButton');


listUl.addEventListener('click', (event) =>{
  if(event.target.tagName == 'BUTTON'){
    if(event.target.className == 'remove'){
        let li = event.target.parentNode;
        let ul = li.parentNode;
        ul.removeChild(li);
    }
    if(event.target.className == 'up'){
        let li = event.target.parentNode;
        let prevLi = li.previousElementSibling;
        let ul = li.parentNode;
       if(prevLi){
        ul.insertBefore(li, prevLi); 
       }
    }
    if(event.target.className == 'down'){  //has the class down
        let li = event.target.parentNode;
        let nextLi = li.nextElementSibling;
        let ul = li.parentNode;
      if(nextLi){
        ul.insertBefore( nextLi, li);
      }
    }
  }
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
```
