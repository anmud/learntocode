# Modifying an Event with Event Modifiers

When working with events there are a couple of things you often will encounter in a real application which you need to solve. As we know `VueJS` makes solving these things easier. 

E.G. We wanna create a kind of a dead spot. And when we hover over this we don't want to update the `coordinates`. We can now setup our own event for the `dead spot`. And we simply want to execute nothing. One solution wil be - still execute a `function` here (we call it `dummy` here in the example). We add this `function` in the `methods object`. In this `function` all we wanna do is just fetch the `event`, which gets passed automatically, and call `stopPropagation` to make sure that it does not **propagate up to elements holding our `span`**. 

**HTML** 

```html
<script src="http://unpkg.com/vue/dist/vue.js"></script>
<div id="app">
    <button v-on:click='increase(2, $event )'>Click me</button>   
    <p>{{counter}}</p>
    <p v-on:mousemove="updateCoordinates">
    Coordinates: {{ x }} / {{ y }}
    - <span v-on:mousemove="dummy">DEAD SPOT</span>  <!--add your own event, and execute a function--> 
    </p> 
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
    },
    dymmy: function(event){
        enent.stopPropogation(); 
    }
    }
});
```

BUT we can do this easier than that. We can remove the `dummy` function. We can still execute nothing in our `event` for the `span` using so called `event modyfier`. It allows us to **modify the behavior of the `event` whenever it comes from**. We add this modyfier by adding a dot (`.`) after the name of the `event` (which we pass as an `argument` to `v-on`). And the modyfier we wanna use here is `stop`, which stops propagation. And we don't need even to execute a `function` here. There are also other modifiers, the probably most important second one would be `prevent`- for running prevent default. We can also chain modifiers `<span v-on:mousemove.stop.prevent="">DEAD SPOT</span>.

**HTML** 

```html
<script src="http://unpkg.com/vue/dist/vue.js"></script>
<div id="app">
    <button v-on:click='increase(2, $event )'>Click me</button>   
    <p>{{counter}}</p>
    <p v-on:mousemove="updateCoordinates">
    Coordinates: {{ x }} / {{ y }}
    - <span v-on:mousemove.stop="">DEAD SPOT</span> 
    </p> 
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