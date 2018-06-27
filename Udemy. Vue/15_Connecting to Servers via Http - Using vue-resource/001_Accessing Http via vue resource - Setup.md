# Accessing Http via vue resource - Setup

For accessing Http one important thing to realise is - `VueJS` is a normal JS code we can mix, embed in normal JS code flow, and that allows us to use any `AJAX libraries`. Now we'll look at a `special package` written for `VueJS` which makes making http requests very easy, which closely embeds it into `Vue instance` and gives some other nice features, it is called - [`Vue resource`](https://github.com/pagekit/vue-resource).

Let's start by installing it. We'll install it via `npm` and let `webpack` bundle this in the end. To do so we'll simply type `npm install` and add `--save` to make sure it is installed as a production dependancy, and `vue-resource` - so, we get `npm install --save vue-resource`. 

After this installed we have to configure it and add it to our application to be able to use it. This is done by using a new `method` on the `global vue object`. In ` main.js` file we can use `Vue.use()`. This basically tells VueJS to add a plugin to the core VueJS functiobality. Also we need to import it. And then we pass this `vue-resource` as an `argument` to `Vue.use()`. And now we are able to access all the `methods` `Vue resource` gives us directly on our `vue instance`. 

**main.js**

```js
import Vue from 'vue'
import VueResource from 'vue-resource';  //import here
import App from './App.vue'

Vue.use(VueResource);        //use method 

new Vue({
  el: '#app',
  render: h => h(App)
})
```
