# Looping through a List of Numbers

To `loop` through `numbers` is qute easy. Let's say we wanna output the `numbers` with a `span`, using `v-for`. We give for exampla `n` name for the number in the `list of numbers`. 

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
<ul>
<li v-for="(ingredient, i) in ingredients">{{ ingredient }} ({{ i }})</li>   
</ul>
<hr>
<ul>
  <li v-for="person in persons">{{person.name}}
    <div v-for="(value, key, index) in person">{{ key }} : {{ value }} ({{ index }})</div>  
  </li>                  
</ul>
<span v-for=" n in 10 ">{{n}}</span>  <!-- loop through the list of numbers -->
<hr>
<template v-for="(ingredient, index) in ingredients">  
<h1>{{ ingredient }}</h1>
<p>{{ index }}</p>
</template>
</div>
``` 