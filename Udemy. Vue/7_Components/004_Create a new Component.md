# Create a new Component

To create a new `component` we need to create a new file in the `src` folder, and we can name it 'Home.vue'. In there we need a `<template>`, <script> and we might need <style>. 

```html
<template>
<p>Server Status: {{status}}</p>
</template> 

<script></script>

<style></style>
```

In the `script` we wanna export an `object`. And here we wanna have our `data` field which is a `function`, where we return the `object` where `status` is set to 'critical'. 

```html
<template>
<p>Server Status: {{status}}</p>
</template> 

<script>
 export default{
     data: function(){
      return {
          status: 'Critical'
      }   
     }
 }
</script>

<style></style>
```

And we wanna have `methods` where we also have an `object` defining our `methods`. And here we can use ES6. 

```html
<template>
<div>
<p>Server Status: {{status}}</p>
<hr>
<button @click='changeStatus'>Change Status</button>
</div>
</template> 

<script>
 export default{
     data: function(){
      return {
          status: 'Critical'
      }   
     },
     methods: {
         changeStatus ()[            //use ES6
             this.status = 'Normal';
         ]
     }
 }
</script>

<style></style>
```
Now we've created our `componenet` and wanna use it. We can either register it globally in the `main.js` file, by saying `Vue.component({})`, giving it a selector and then the `object`. For that we will need an import, let's name it 'Home'. 

```js
import Vue from 'vue'
import App from './App.vue'
import Home from './Home.vue'

Vue.component('app-server-status', Home);   //register globally

new Vue({
  el: '#app',
  render: h => h(App)
})
```
Now with this setup we can use `app-service-status` as a selector in our whole application, in `App.vue` root file.  