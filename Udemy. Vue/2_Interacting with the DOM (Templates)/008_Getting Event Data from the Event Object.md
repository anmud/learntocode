# Getting Event Data from the Event Object

The important thing about `events` is - the default `event object` we can listen to. This `event object` is created by JS and holds some information. And also automatically gets passed to each `function` we execute through VueJs. Let's say we wanna access this information, cos we might be interested in outputing this data. 

**HTML** 

```html
<script src="http://unpkg.com/vue/dist/vue.js"></script>
<div id="app">
    <button v-on:click='increase'>Click me</button>
    <p>{{counter}}</p>
    <p>Coordinates: {{ x }} / {{ y }}</p> <!--we want to output some coordinates-->
</div>
```

We setup these coordinates in VueJS

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
    increase: function(){
        this.counter ++;
    }
    }
});
```

And then hovering over our `paragraph` we wanna update these two `values`. 


**HTML** 

```html
<script src="http://unpkg.com/vue/dist/vue.js"></script>
<div id="app">
    <button v-on:click='increase'>Click me</button>
    <p>{{counter}}</p>
    <p v-on:mousemove="updateCoordinates">Coordinates: {{ x }} / {{ y }}</p> <!--set directive to update coordinates-->
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
    increase: function(){
        this.counter ++;
    },
    updateCoordinates: function(event){  //method to use in event
     this.x = event.clientX;
     this.y = event.clientY;
    }
    }
});
```