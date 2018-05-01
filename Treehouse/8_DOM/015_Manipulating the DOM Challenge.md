# Manipulating the DOM Challenge

1. Set the text of the `<h1>` element
2. Set the color of the `<h1>` to a different color
3. Set the content of the `.desc` paragraph. The content should include at least one HTML tag
4. Set the class of the `<ul>` to `list`
5. Create a new `list` item and add it to the `<ul>`
6. Change all `<input>` elements from text fields to checkboxes
7. Create a `<button>` element, and set its text to `Delete`. Add the `<button>` inside the `.extra` `<div>`
8. Remove the `.extra` `<div>` element from the DOM when a user clicks the `Delete` button

**HTML**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <link rel="stylesheet" href="css/main.css">
  <title>Practice Manipulating the DOM</title>
 </head>
<body>
  <div class="container">
    <h1 id="first-heading"></h1>
    <p class="desc"></p>
    <ul>
      <li><input> Play music</li>
      <li><input> Swim</li>
      <li><input> Bike ride</li>
      <li><input> Code</li>
    </ul>
    <div class="extra">
      <p>This is extra content you need to delete.</p>
    </div>
  </div>
  <script src="js/scripts.js"></script>
</body>
</html>
```
### Solution

**JS**
```js
// 1: Set the text of the <h1> element
let h1Text = document.querySelector('h1#first-heading');
h1Text.textContent = "My activities list";


// 2: Set the color of the <h1> to a different color

h1Text.style.color = "red";

// 3: Set the content of the '.desc' paragraph
// The content should include at least one HTML tag

let pContent = document.querySelector('p.desc');
pContent.innerHTML = "A list of <strong>fun</strong> things I want to do today";

// 4: Set the class of the <ul> to 'list'

let myUl = document.querySelector('ul');
myUl.className = "list";
                              
// 5: Create a new list item and add it to the <ul>

let li = document.createElement('li');
li.innerHTML = "<input> Eat ice cream";
myUl.appendChild(li);


// 6: Change all <input> elements from text fields to checkboxes

let input = document.getElementsByTagName('input');
for(let i = 0; i < input.length; i += 1){
  input[i].type = "checkbox";
}


// 7: Create a <button> element, and set its text to 'Delete'
// Add the <button> inside the '.extra' <div>
let removeDivButton = document.createElement('button');
let extraDiv = document.querySelector('div.extra');
extraDiv.appendChild(removeDivButton);
removeDivButton.textContent = "Delete";

// 8: Remove the '.extra' <div> element from the DOM when a user clicks the 'Delete' button
let containerDiv = document.querySelector('div.container');
removeDivButton.addEventListener('click', () =>{
containerDiv.removeChild(extraDiv);                                 
});
```


