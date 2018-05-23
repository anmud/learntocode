# Keeping Track of Elements when using `v-for`

It's important to understand what happens behind the scenes when we `loop`, if VueJS need to update one of these `values`, cos somewhere of our code we change our `elements`. 

Let's say we wanna add a new `ingredient` to our `list` by clicking a `button` - which simply pushes the `item` in the `array`. 

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
<ul>
<li v-for="(ingredient, i) in ingredients">{{ ingredient }} ({{ i }})</li>   
</ul>
<button @click="ingredients.push('spices')">Add New</button>              <!-- add a new item -->
<hr>
<ul>
  <li v-for="person in persons">{{person.name}}
    <div v-for="(value, key, index) in person">{{ key }} : {{ value }} ({{ index }})</div>  
  </li>                  
</ul>
<span v-for=" n in 10 ">{{n}}</span>  
<hr>
<template v-for="(ingredient, index) in ingredients">  
<h1>{{ ingredient }}</h1>
<p>{{ index }}</p>
</template>
</div>
```

**Two important things are to be noted here:**

1. VueJS conviently proxies this `push` method here, cos generally the `push` method doesn't create a new `array`, it just adds `items` to the existing one. And then it's a bit hard to track since the `object` itself, the `array` doesn't change here, cos it is a `reference type` and the pointed to the type hasn't changed - only the `value` in memory, but for that to realise, we have to watch this `value`. Which VueJS does for us automatically. 

2. How does VueJS update the `list` if something need to be changed? It updates the `list` by simply updating the position in the `array` where is something changed. It doesn't keep track of the specific `element` it created it will only patch it in the second position. Most of times this is the behavior we want.

But if we wanna be super safe and wanna make sure that VueJS is not only aware of the position, but of the actual `list item` (on which the `value`, we are working with, sits), we need to assign a unique `key` to this `list item`. We do this by using `v-bind` syntax, and passing a unique `key`. A better `key` will be a real unique `value`. For example, if we know that each `ingredient` will occur in our `list` once, we can use `ingredient` as a `key`. 

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
<ul>
<li v-for=" (ingredient, i) in ingredients :key="ingredient" ">{{ ingredient }} ({{ i }})</li>   
</ul>
<button @click="ingredients.push('spices')">Add New</button>              <!-- add a new item -->
<hr>
<ul>
  <li v-for="person in persons">{{person.name}}
    <div v-for="(value, key, index) in person">{{ key }} : {{ value }} ({{ index }})</div>  
  </li>                  
</ul>
<span v-for=" n in 10 ">{{n}}</span>  
<hr>
<template v-for="(ingredient, index) in ingredients">  
<h1>{{ ingredient }}</h1>
<p>{{ index }}</p>
</template>
</div>
```

Now behind the scenes we are now safe -  VueJS not only stores the `position` of the `element` but the `element` itself. Which means should we ever need to re-order `elements` or do smth like that, it will take the actual `element` to reorder it and not just override the `values` in some of the positions. 