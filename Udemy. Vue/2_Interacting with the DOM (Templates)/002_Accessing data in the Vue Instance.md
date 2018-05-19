# Accessing data in the Vue Instance

**HTML**

```html
<script src=="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<div id="app">
<p>{{ sayHello() }}</p>
</div>
```
**JS**

```js
new Vue ({
el : '#app'
data : {
    title : 'Hello World!'
}
methods : {
    sayHello: function(){
        return this.title; 
    }
}
})
```
In our `Vue instance` if we want to output the `title` we should return the `title` using `this` keyword, so `Vue instance` understands it should look for the `title` property inside itself. VueJs provides some magic here! It proxies these `properties` in a way that by simply calling `this` anywhere in our `Vue instanse object` will give us access to these proxied `properties`. So, behind the scenes VueJS creates a kind of easy access for us. 
