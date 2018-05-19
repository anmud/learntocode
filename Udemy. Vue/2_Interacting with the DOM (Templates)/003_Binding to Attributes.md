# Binding to Attributes

Let's say we have a `link` property and it stores a link to google.com. In our `paragraph` we also might want to output this link. So, in our `html` we could enter our `anchor` tag and call it "Google" since this `link` leads to google. And then we could try to follow it using `{{}}` in our `href` attribute, to then output the `link`. 

**HTML**

```html
<script src=="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<div id="app">
<p>{{ sayHello() }} - <a href="{{ link }}">Google</a></p>
</div>
```
**JS**

```js
new Vue ({
el : '#app'
data : {
    title : 'Hello World!',
    link: 'http://google.com'
}
methods : {
    sayHello: function(){
        return this.title; 
    }
}
})
```

#### **BUT** 
This doesn't work correctly. We can't use `{{}}` in any html `attribute`!!!!!!!!!
Instead we can bind our `link` dynamically by introducing a `directive` VueJS shifts with. This `directive` is called `v-bind`. This `directive` tells VueJS : "Don't use the normal attribute, instead bind it". We do pass an `argument` to the `v-bind` directive by adding a colon `:`, and the `argument` we do pass is the name of the `attribute` we wanna bind. Now we can set `link` between the quotation marks. 

**HTML**

```html
<script src=="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<div id="app">
<p>{{ sayHello() }} - <a v-bind:href="link">Google</a></p>  <!--directive here-->
</div>
```