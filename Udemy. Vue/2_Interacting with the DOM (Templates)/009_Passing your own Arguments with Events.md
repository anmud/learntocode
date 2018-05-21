# Passing your own Arguments with Events

Now we inrease our `counter` by `1`, what if we want to add our own step? We can do this by passing our own `argument`. 

**HTML** 

```html
<script src="http://unpkg.com/vue/dist/vue.js"></script>
<div id="app">
    <button v-on:click='increase(2)'>Click me</button>   <!--pass an argument-->
    <p>{{counter}}</p>
    <p v-on:mousemove="updateCoordinates">Coordinates: {{ x }} / {{ y }}</p> 
</div>
```
Now in our `increse` function we should listen to `step`

**JS**

```js
new Vue({
    el: '#app',
    data: {
     counter: 0,
     x: 0,
     y: 0
    },
    methods:{
    increase: function(step){ 
        this.counter += step; //we increase our counter by a step we set 
    },
    updateCoordinates: function(event){  
     this.x = event.clientX;
     this.y = event.clientY;
    }
    }
});
```

What if we want to pass both - our own `argument` and automatically created `event object`? We can add a second `argument` and here **the naming** is important!!!! VueJS automatically fetches this  `default event argument` and stores it in a kind of a `variable`, named `$event`. 

**HTML** 

```html
<script src="http://unpkg.com/vue/dist/vue.js"></script>
<div id="app">
    <button v-on:click='increase(2, $event )'>Click me</button>   <!--add a second argument-->
    <p>{{counter}}</p>
    <p v-on:mousemove="updateCoordinates">Coordinates: {{ x }} / {{ y }}</p> 
</div>
```

**JS**

```js
new Vue({
    el: '#app',
    data: {
     counter: 0,
     x: 0,
     y: 0
    },
    methods:{
    increase: function(step, event){ 
        this.counter += step;  
    },
    updateCoordinates: function(event){  
     this.x = event.clientX;
     this.y = event.clientY;
    }
    }
});
```