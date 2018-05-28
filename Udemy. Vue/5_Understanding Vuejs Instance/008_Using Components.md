# Using Components

What if we wanna create a reuseble `component` to add a `template` in different places of the page?
We can create such a component, with registering one with `Vue.component`. `Vue.component` takes as the first `argument` the `selector` of the `component`, and the second `argument` is the JS `object` which is similar ot the `object` we pass to the `vue instance`, but not equal, for example `data` is used differently. 


**JS**

```js
var data = {                   
    title: 'The VueJS Instance',
    showParagraph: false}

Vue.component('hello', {                //create a component
    template: <h1>Hello!</h1>
});

var vm1 = new Vue({
  el: '#app2',
  data: data,    
  methods: {
    show: function() {
      this.showParagraph = true;
      this.updateTitle('The VueJS Instance (Updated)');
    }
```

Now we can use this `component` everywhere, e.g in our `app2`  

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app1">
  <h1 ref="heading">{{ title }}</h1>
  <button v-on:click="show" ref="myButton">Show Paragraph</button> 
  <p v-if="showParagraph">This is not always visible</p>
</div>

<div id="app2">
  <h1 ref="heading">{{ title }}</h1>
  <button v-on:click="onChange">Change something in Vue 1</button>
  <hello></hello>
  <hello></hello>
</div>

<div id='app3'>    

</div>
```
