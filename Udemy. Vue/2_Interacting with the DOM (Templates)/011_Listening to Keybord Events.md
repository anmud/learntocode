# Listening to Keybord Events

We also have `key modifiers`. 

### Example

In our `input` field we wanna listen to `keyup` event, which obviously is fired whenever the user releases the `key` and the `key` goes up. And here we wanna throw an `alert`. And in the `methods` property we add an `alertMe` function. This `function` should be executed when the user type something in the `input` field. 

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
    <input type:'text' v-on:keyup="alertMe">   <!--listen to keyup event--> 
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
    alertMe: function(){
     alert('Alert!');  //alert function here 
    }
    }
});
```

But this is generally not the best experience. Maybe we wanna only send an `alert` if we submit, hit enter let's say. We can add a `key modyfier` for this, using a dot (`.`) and the name of the key.  This enables us to only listen to a specific keys. 

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
    <input type:'text' v-on:keyup.enter="alertMe">   <!--add a key modyfier--> 
</div>
```

##### Find [KEY MODIFIERS](https://vuejs.org/v2/guide/events.html#Key-Modifiers) here!