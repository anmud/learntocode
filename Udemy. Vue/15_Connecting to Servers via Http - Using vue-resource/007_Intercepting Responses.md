# Intercepting Responses

What if we also want to have a look at the `response`? Generally we can look at the `response` accessing our `next()` function and pass `argument` to it. This `argument` also has a `function` where we will get the `response` as an argument, and then we can use the `response` here with `json`, be careful with this, cos this will affect all your requests (we may not really do this in the production app), but in a case we do need to change sertain parts about the `response` this is how we can do it. We need to extract some kind of `object` again which we can loop through all the keys. All we wanna do inside the `function` - to return a new `object`, where we have key, let's name them "messages" whish is equal to our response body. 

**main.js**
```js
import Vue from 'vue'
import VueResource from 'vue-resource'; 
import App from './App.vue'

Vue.use(VueResource); 

Vue.http.options.root = 'https://vuejs-http-baec0.firebaseio.com/data.json'      

Vue.http.interceptors.push( (request, next) => {
    console.log(request);
    if(request.method == 'POST'){
     request.method = 'PUT'
    }
    next( response => {
     response.json = () => {
     return { messages: response.body }
     }
    });
});

new Vue({
  el: '#app',
  render: h => h(App)
})
```

This now allows us to extract our `response body`, but store it in a separate `object` which has extra `key` for that ("messages"), so that looping through the `keys` and extracting the `user` as the `value` of that key,will work again. 