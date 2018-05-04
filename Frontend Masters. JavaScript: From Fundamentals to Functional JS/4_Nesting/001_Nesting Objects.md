# Nesting Objects

`innerBox` is a property in `box` that contains a `value` that is also an `object`. So, this is a nested `object`.

```js
var box = {};
box['innerBox'] = {}; //we can have innerbox inside our box
```
![nesting-objects1](../nesting-objects1.png) 

```js
var box = {};
box['innerBox'] = {}; //we can have innerbox inside our box
box['innerBox']['full'] = true; //we can create for the innerbox, the property - full : true
```
![nesting-objects2](../nesting-objects2.png) 

**NOTE** Rules don't channge. We can also use `dot-notation`.

```js
var box = {};
box['innerBox'] = {}; 
box['innerBox'].full = true;
```






