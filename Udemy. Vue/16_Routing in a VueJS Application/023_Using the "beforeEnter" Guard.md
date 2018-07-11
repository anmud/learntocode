# Using the "beforeEnter" Guard

Let's start with the task  if the user visit a certain `route`. We have **three different places** to setup if the `user-allowed-to-enter` check and one place where we may setup is `user-allowed-to-leave` check. 

The first place to set if `user-allowed-to-enter` check is in the `main.js` file. When we setup our `router`, we can use our `router`, access it before we assign it to the `vue-instance` and setup `beforeEach()` method. The `beforeEach()` method means execute this before each routing action. This `method` expect to get a `function` as an argument, which gets its own arguments: `to`, `from` and `next` - this function is a callback which we can execute to let the request continue its journey. So, basically this `beforeEach` function gets executed on each routing action. So, we may use this only for very generic checks and we should be aware that it gets executed all the time. **Important** - we have to execute `next()` to allow the routing action to continue, if we don't do that it's assumed that it's not allowed to continue, and it will exit, won't to the `route`/page we wanna it to go to. Alternatively we could pass to `next()` `false` argument - `next(false)` - to stop the current operation and stay at the page we were at. Or we can either pass a `path` - `next('/')` - or the same `object` from `router-links` and `router push method` (`<router-link :to="{ name: 'userEdit', params: {id:$route.params.id}, query: {locale: 'en', q: 100} }" >Edit User</router-link>`), so the `object` where we define the `path` we want to navigate to.

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
  if (savedPosition){                
  return savedPosition; 
  }
  if (to.hash){                     
  return { selector: to.hash};
  }
  return {x: 0, y: 0};           
  }
});

router.beforeEach( (to, from, next) => {      //add beforeEach to the router
console.log('global beforeEach');
next(); 
}); 



new Vue({
  el: '#app',
  router,
  render: h => h(App)
})
```
Sometimes, we want to protect certain `routes`. Let's say we wanna protect our `UserDetail` route, then we can add one more property - `beforeEnter` to the `routes` in the `routs.js`.  `beforeEnter` is a `function` (which you could also store in another file and import), it has the same `arguments`: `to`, `from` and `next` and works exactly the same way, just like in global `function`, but now directly limited to one `route`. 

**routes.js**

```js
import User from './components/user/User.vue';
import UserStart from './components/user/UserStart.vue';
import UserEdit from './components/user/UserEdit.vue';
import UserDetail from './components/user/UserDetail.vue';
import Home from './components/Home.vue';
import Header from './components/Header.vue';

export const routes = [
{ path: '',  name: 'home', components: {default: Home, 'header-top': Header} },
{ path: '/user', components: { default: User, 'header-bottom': Header }, children: [
{ path: '', component: UserStart},
{ path: ':id', component: UserDetail, beforeEnter: (to,from,next)=>{    //add beforeEnter property
console.log('inside route setup');
next();
}  },
{ path: ':id/edit', component: UserEdit, name: 'userEdit'}
] },
{path: '/redirect-me', redirect: '/user' },
{ path: '*', redirect: '/' }  
];
```

The last place where we can implement that is directly in the `component` we are navigaving to - in our case `UserDetail`. For that we go to the `instance` and there we got two new mwthods available. One of them is `beforeRouteEnter()`, and if we call `next()` we finally load this `component`. **The important key to understand here**  - as long as we don't call `next()` here, this `component` is not loaded, this also means that in this lifecycle hook we can't access our `vue instance`, the `data object`. For example, if we wanna access our `link property` in the `data object`:  `beforeRouteEnter(to, from, next) { this.link;  next(); }`  - it would not work, because this component hasn't been created yet. This is kind of a special case here - we are in this file, but the `object` doesn't fully initialised, so we can't access it. In case we absolutely need to access it, we can pass a callback to the `next()` function, where we pass our `vue model` and in there we can access the `property` from the `data object`. This is now a place where we do have access to the `component` cos since it is inside the `next()` function it's simply a callback, we pass it as an `argument`, which is executed once this `component` has been loaded. But this also means that at this point of time the `component` has been created. 

```js
beforeRouteEnter(to, from, next){
    next(vm => {
    vm.link;
    });
    }
```

If we really want to check if this `component` should be created before creating it, then we have to do this outside the `next()` callback. And here we don't have access to the component's `data object`. So, we check if the user is authenticated, for exaple access some other file, some global service where we store this (`if(true)` to always allow navigation), if this the case we'll execute `next()` and if not then we call `next(false)` to stop. 

**UserDetail**

```html
<template>
<div>
    <h3>Some User Details</h3>
    <p>User loaded has ID: {{ $route.params.id }}</p>
     <router-link  
     tag="button" 
     :to="link"     
     class="btn btn-primary">Edit User</router-link>  
</div>
</template>

<script>
export default {
    data(){
        return{
            link: {                    
                name: 'userEdit', 
                params: {id: this.$route.params.id},  
                query: {locale: 'en', q: 100},
                hash: '#data'             
                }
        }
    },
    beforeRouteEnter(to, from, next){
    if (true){
        next();
    }else{
     next(false);
    }
    
    }
}
</script>
```
So, this is how we can check if a user is allowed to visit a certain page, we can check it in three different places depending on which access we need. Important to keep in mind - in all three places we don't have access to the `component` we are passing it to , we only have access to the `router` we are coming from and the `route` we are going to, and we have a `callback function` which we need to execute to either abort or redirect or let the request continue. 