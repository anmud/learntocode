# Parent vs Child Scope

What if we have a `function` nested inside of another `function`? How does that affect our scope. 

```js
var g = 'global'; 

function blender(fruit) { 
  var b = fruit; 
  var y = 'yogurt';
 
  function bs() { 
    alert( b + ' and ' + y + ' makes ' + b + ' swirl'); 
  } 
  bs(); 
} 

blender('blueberry');
```

Actually, `child scope` (in the nested `function`) has access to the `parent scope` as well as to `global scope` BUT the `parent scope` don't have access to the `child scope`. 

So in our example if we add one more `variable` ('x') to the nested `function` and try to `console.log` it from the parent `funcion` - it will give us an error. 

```js
var g = 'global'; 

function blender(fruit) { 
  var b = fruit; 
  var y = 'yogurt';
 
  function bs() { 
      var x = 'asdf'
    alert( b + ' and ' + y + ' makes ' + b + ' swirl'); 
  } 
  console.log(x) //ERROR
  bs(); 
} 

blender('blueberry');
```
There is the only way to create `private variables` - is by storing them in the `function`. 