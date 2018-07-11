# Controlling the Scroll Behavior

Configuring the `scrolling behavior` in `vue router` is simple. We go to the `main.js` file where we setup the `router` and there we can pass another property, the `scrollBehavior` property - that is actuallya `method`, and here we can configure how we want it to behave. This `method` has three `arguments`: `to`, `from` and `savedPosition`. This `function` expects to get back either an `object` where we have `x` and `y` coordinates where we then specify where to go: e.g `return {x: 0, y: 700}`, or a `selector`. 

**main.js**

```js
import Vue from 'vue'
import VueRouter from 'vue-router';
import App from './App.vue'
import { routes } from './routes';

Vue.use(VueRouter);

const router = new VueRouter({
  routes,
  mode: 'history',
  scrollBehavior (to, from, savedPosition){            //set the scroll behavior property 
  return {x: 0, y: 700}
  }
});

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```

So, the alternative is to use a `selector`. We first check with the `condition` if the `route` we wanna navigate to has the `hash` property being set, so this is not empty, in this case we want to return an `object` where we say `selector` and use the `hash` which is a string - this will give us a place to navigate to. And if we have this condition, we'll scroll down. 

**main.js**

```js
import Vue from 'vue'
import VueRouter from 'vue-router';
import App from './App.vue'
import { routes } from './routes';

Vue.use(VueRouter);

const router = new VueRouter({
  routes,
  mode: 'history',
  scrollBehavior (to, from, savedPosition){            
  if (to.hash){                     //check the condition first
  return { selector: to.hash};
  }
  return {x: 0, y: 700};           //scroll down
  }
});

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```

Finally, the final step we might want to include, to check if the `savedPosition` is set because if the user navigated back with the `back button` it's probably not the desired behavior to scroll him all the way down/up or whatever; you maybe want to scroll him to the position he was at. And only if this is not set, we check if the `hash` is set, and only if this is not set then we may be scroll the user up all the way to the top of the page. 

**main.js**

```js
import Vue from 'vue'
import VueRouter from 'vue-router';
import App from './App.vue'
import { routes } from './routes';

Vue.use(VueRouter);

const router = new VueRouter({
  routes,
  mode: 'history',
  scrollBehavior (to, from, savedPosition){            
  if (savedPosition){                 //set the saved position
  return savedPosition; 
  }
  if (to.hash){                     
  return { selector: to.hash};
  }
  return {x: 0, y: 0};          //scroll up 
  }
});

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```
