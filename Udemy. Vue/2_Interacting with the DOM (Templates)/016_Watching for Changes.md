# An alternative for `computed` property: Watching for Changes

In working with dependances VueJS also has a number of ways doing this. We can use also the `watch` object (execute code upon data changes). As a `key` we set the `property` name we wanna watch - so, this has to match one of our properties. Then as a `function` we specify the code we wanna execute whenever the `counter` changes. And JS automatically passes the `value` of the upcoming change.  
This allows us to react to changes. 
NOTE! It is the best practise to use `comuted` properties wherever you can, simply because they are more optimised. But there are cases when you need to react to every change, although there is a number of cases where `computed` properties won't do the trick. And that is if we need a synchronous tasks to be run. `Computed` properties always ned to run synchronously, which means we are returning something and that needs to happen ASAP or immediately, there is no way you can reach out to a server or do some asynchronous task inbetween. If we need to run such a task we need to run some other code, which triggers when the `property` updates, and which is not solved by a `computed` property - then we should use `watch`. 
E.G we can reset the `counter` after two seconds.  


**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <button v-on:click="counter++">Increase</button> 
  <button v-on:click="counter--">Decrease</button> 
  <button v-on:click="secondCounter++">Increase Second</button>
  <p>Counter: {{ counter }} {{ secondCounter }}</p>
  <p>Result: {{ result() }} | {{ output }}</p>  
</div>
```

**JS**

```js
new Vue({
	el: '#app',
  data: {
  	counter: 0,
    secondCounter: 0
  },
  computed: {
  	output: function() {
    	console.log('Computed');
    	return this.counter > 5 ? 'Greater 5' : 'Smaller than 5'; 
    }
  },
  watch:{
   counter: function(value){
       var vm = this;   //we have to store our vue instance in a separate variable
      setTimeout(function(){
       vm.counter = 0;  
      }, 2000)  //to reset the counter, function inside is a closure
  },
  methods: {
  	result: function() {               
    	console.log('Method');
    	return this.counter > 5 ? 'Greater 5' : 'Smaller than 5';
    }
  }
});
```