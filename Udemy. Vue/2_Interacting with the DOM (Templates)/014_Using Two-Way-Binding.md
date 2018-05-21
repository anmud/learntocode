# Using Two-Way-Binding

What if we want `output data` and listen to `events` at the same time? E.G. we have an ` input` field and we wanna populate this `input` field with the name of the `user` and on the same time whenever the user changes the `input` field we wanna update the `data` property, and updade it everywhere we output it in our code. All we need to do is to **add `v-model` directive** to this `input` element. The `v-model` directive tells VueJS setup to the data binding for the `input`, and between the quotation marks - the `property` which you want to bind in both directions. So, wat this will do is - it will, on the one hand, output the `name` in the `input` field, but on the other hand, whenever we change it in the `input` it will listen to these changes and update the `name property` in our `vue instance`, that's reflecting this change in all the places where we also use the `name instance` - in our example in the `paragraph`.   

**HTML**

```html
<script src="http://unpkg.com/vue/dist/vue.js"></script>
<div id="app">
    <input type="text" v-model="name">   <!--v-model directive here-->
    <p>{{name}}</p>
</div>
```
**JS**

```js
new Vue ({
    el: '#app',
    data: {
        name: 'Max'
    }
});
```