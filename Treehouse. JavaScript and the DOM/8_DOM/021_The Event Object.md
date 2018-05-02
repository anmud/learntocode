# The Event Object

Here, you'll learn how to add an `event listener` to a `parent element` and let it handle events on its `children`.


Here is [MDN page for the Event Object](https://developer.mozilla.org/en-US/docs/Web/API/Event)
Here is [MDN page for the tagName property](https://developer.mozilla.org/en-US/docs/Web/API/Element/tagName)

Well, how does the `parent element` knows which `child` trigger the event? When an `event handler` is called it recieves `event object` as its first argument. This `object` has some useful information about the `event`. As well as a few `methods` we can use to help us handle the `event` inside the `handler`. 

```js
eventTarget.addEventListner('click', (event)=>{
    //event is an object with info and methods
});
```

In our example we first need to add the `event` parameter so the `event object` will be available inside the `handlers`.
Then we need to get a specific `element` that is triggering the event. We can use `target` property for the `event object`. And we want this effect to affect the `list items` only. Let's add `if statement`.
```js
const toggleList = document.getElementById('toggleList');
const listDiv = document.querySelector('.list');
const input = document.querySelector('input');
const p = document.querySelector('p.description');
const button = document.querySelector('button');
const addItemInput = document.querySelector('input.addItemInput');
const addItemButton = document.querySelector('button.addItemButton');
const removeItemButton = document.querySelector('button.removeItemButton');


listDiv.addEventListener('mouseover', (event) =>{ //add event parameter
    if(event.target.tagName == 'LI'){                                                 
event.target.textContent = event.target.textContent.toUpperCase();//use target property
}  
});

listDiv.addEventListener('mouseout', (event) =>{    //add event parameter
     if(event.target.tagName == 'LI'){        
event.target.textContent = event.target.textContent.toLowerCase();  //use target property
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

removeItemButton.addEventListener('click', () =>{
let ul = document.getElementsByTagName('ul')[0];                               
let li = document.querySelector('li:last-child'); 
ul.removeChild(li);
});
```