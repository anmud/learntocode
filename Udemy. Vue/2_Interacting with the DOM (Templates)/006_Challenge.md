# Challenge

**Tasks**

1. Fill the <p> below with your Name and Age - using Interpolation -->
2. Output your age, multiplied by 3 -->
3. Call a function to output a random float between 0 and 1 (Math.random()) -->
4. Search any image on Google and output it here by binding the "src" attribute -->
5. Pre-Populate this input with your name (set the "value" attribute) -->
    
### Solution

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="exercise">
   <!-- 1) Fill the <p> below with your Name and Age - using Interpolation -->
    <p>VueJS is pretty cool - {{ name }} ({{ age }})</p>
    <!-- 2) Output your age, multiplied by 3 -->
    <p>{{ multiply() }}</p>
    <!-- 3) Call a function to output a random float between 0 and 1 (Math.random()) -->
    <p>{{ randomNumber() }}</p>
    <!-- 4) Search any image on Google and output it here by binding the "src" attribute -->
    <div>
     <img v-bind:src="image" style="width:100px;height:100px">
    </div>
    <!-- 5) Pre-Populate this input with your name (set the "value" attribute) -->
    <div>
        <input type="text" v-bind:value = "name">
    </div>
</div>
```
**JS**

```js
new Vue({
    el: '#exercise',
    data: {
        name: 'Ana Mo',
        age: '33',
        image: 'https://www.pinterest.com/pin/453174781240424242/'
    },
    methods: {
    multiply: function(){
    return this.age * 3;
    },
    randomNumber: function(){
    return Math.random();
    }
    }
    
})
```