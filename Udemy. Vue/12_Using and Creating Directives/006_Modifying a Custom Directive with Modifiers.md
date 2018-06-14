# Modifying a Custom Directive with Modifiers

Well, what if we also wanna add a `modifyer`. First, what a `modifyer` could do in our example? What if wanna change the style delayed? 

Therefore we can add the `delayed` modifier and surely we need create it in our `main.js` first. 

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Built-in Directives</h1>
                <p v-text=" 'Some text' "></p>  
                 <p v-html=" '<strong>Some strong text</strong>' "></p>  
            </div>
        </div>
        <hr>
<div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Custom Directives</h1>
                <p v-highlight:background.delayed=" 'red' ">Color this</p>  <!--add a modifyer-->
            </div>
        </div>
    </div>
</template>

<script>
    export default {
    }
</script>

<style>

</style>
```
In our `main.js` we want to check if we got the `modifyer`. Therefore we set a `variable delay` which is zero by default (no delay), and then we wanna check if the `binding` has `modifiers`. `modifiers` is an `array` and there we wanna check if it has the `delayed` key here. That allows us to add a `setTimeout()` function, where we will wait for the delay and in the `callback function` we will execute the code we had before - with setting the `value` and the `argument`. 

**main.js**

```js
import Vue from 'vue'
import App from './App.vue'

Vue.directive('highlight', {    
 bind(el, binding, vnode){    
 var delay = 0;  
 if (binding.modifiers['delayed']) {
     delay = 3000;
 }     
 setTimeout( ()=>{
if(binding.arg == 'background'){
 el.style.backgroundColor = binding.value
 }else{
     el.style.color = binding.value
 }
 },delay);
 }
});

new Vue({
  el: '#app',
  render: h => h(App)
})
```