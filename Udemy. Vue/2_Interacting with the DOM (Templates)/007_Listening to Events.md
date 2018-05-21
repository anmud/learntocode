# Listening to Events

We wanna hook the `button` so when we click on it, it increases the `counter`. To do this we use `v-on` directive, which listens to the `events`. Well, we listen to something to recieve something from our template. `v-on` takes an `argument` which is the name of the `event`. We can use, actually, any `DOM event` existent for a `button` (e.g 'mouse-enter' or 'mouse-leave', etc.). Then we should assign to the `argument` the code we want to execute when clicking on this `button`. 

**HTML** 

```html
<script src="http://unpkg.com/vue/dist/vue.js"></script>
<div id="app">
    <button v-on:click='increase'>Click me</button>
    <p>{{counter}}</p>
</div>
```
**JS**

```js
new Vue({
    el: '#app',
    data: {
     counter: 0
    },
    methods:{
    increase: function(){
        this.counter ++;
    }
    }
});