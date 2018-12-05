# Updating Objects, in an immutable way

How to update existing `property` in  JS `objects` in `an immutable way`?

Use `spread operator (...)`. If you want to update the existing property use the `new value` of a `property` after the `spread operator`. 

```js
const meal = {
description: 'breakfast',
id: 1
}

const updatedMeal = {
...meal,
description: 'snack'                         
} 

console.log(updatedMeal) // outputs: { description: 'snack', id: 1}
```



**HTML**

```html
<script src=="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<div id="app">
<p></p>
</div>
```

In order to manipulate the `html` template we need to create in JS a new `Vue instance`. `Vue instance` is the core of each `Vue` application, of each of piece of code you wanna use `Vuejs` in. We create such instances and then these instances have one major job - controle theis own template of code of `html code` which they render to the screen. In order to do this we need to pass an `argument` in our `Vue()` constructor `function`. The `argument` is a JS `object`. And there we have one very important `property` `Vuejs` will recognise - an `element`. `El` takes a string as a `value`. And with this `string` we setup which part of our html code should be under controle of our `vue instance`. Under control here means - we can change it through `vue instance`. 

**JS**

```js
new Vue ({
el : '#app'
})
```
![vue-instance](../vue-instance.png)
