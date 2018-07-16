# Setup Project Routes

To setup our `routes` lets first install `vue-router` - `npm install --save vue-router`. Then we'll create `routes.js` file where we put all our routes. In our `main.js` we import `vue-router`, use this `router` - calling `Vue.use(VueRouter)`, next we'll need to setup the `router` and for that first we need to create some routes in the `routes.js` file. 

**main.js**
```js
import Vue from 'vue';
import VueRouter from 'vue-router';
import App from './App.vue';

Vue.use(VueRouter);

new Vue({
  el: '#app',
  render: h => h(App)
})
```
So, we need three `routes`: to the `home page`, to the `portfolio page` and to the `stocks page`. So, we import these component to the file and create a `constant` which will hold our `routes` so we can export them later. Routes should have their `paths`. 

**routes.js**
```js
import Home from './components/Home.vue';
import Portfolio from './components/portfolio/Portfolio.vue';
import Stocks from './components/stocks/Stocks.vue';


export const routes = [
    { path: '/', component: Home },
    { path: '/portfolio', component: Portfolio },
    { path: '/stocks', component: Stocks }
]
```

Then we should go back to our `main.js` file and import our `routes` there. And we can now use our `router` by running a `new VueRouter()` and there we'll pass an `object` where we configure our `router`. And finally add the `router` to our `vue instance`. 

**main.js**
```js
import Vue from 'vue';
import VueRouter from 'vue-router';
import App from './App.vue';
import {routes} from './routes.js';

Vue.use(VueRouter);

const router = new VueRouter({
  routes,
  mode: 'history'
});

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```
Now to see our `router` in action we go to our `App.vue` file and add a first `<router-view>` - the place we then can load our `routes. With that in place  

**App.vue**
```html
<template>
<div class="container">        
        <div class="row">
            <div class="col-xs-12">
        <router-view></router-view>
        </div>
     </div>
 </div>
</template>

<script>
    
</script>

<style>

</style>
```