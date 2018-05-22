# Dynamic Styling with CSS Classes: Basics

Let's talk about attaching `CSS Classes`. 

### Example

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <div class="demo"></div>
  <div class="demo"></div>
  <div class="demo"></div>
</div>
```

**JS**

```js
new Vue ({
    el: '#app'
});
```

**CSS**

```css
.demo {
 width: 100px;
 height: 100px;
 background-color: grey;
 display: inline-block;
 margin: 10px;
}
```
Note, no VueJS code involved here al all. 

![vue-with-css-classes](../vue-with-css-classes.png)


It's interesting to see how we can attach `classes` to these `divs`. Let's create three more `classes`. 

**CSS**

```css
.demo {
 width: 100px;
 height: 100px;
 background-color: grey;
 display: inline-block;
 margin: 10px;
}
.red {                      /*one more class here*/
background-color: red;
}
.green {                   /*one more class here*/
background-color: red;
}
.blue {                   /*one more class here*/
background-color: red;
}
```

Now we can use these three new `classes` in our app. Let's see what VueJS can do for us. Let's say we wanna attach this `red block` only if we click on this `element`, and detach it if we click again. 
To be able to show this we add a `data` property to our `vue instance`, and inside we'll setup a new `property`. And initially we set it to `false` to say: 'No, we don't want ot set it initially'. Upon click on it we wanna set `attachRed` to the opposite. 

**JS**

```js
new Vue ({
    el: '#app',
    data: {
    attachRed : false //new property here 
    }
});
```

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <div class="demo" @click="attachRed = !attachRed"></div> <!--set attachRed to the opposite after clicking-->
  <div class="demo"></div>
  <div class="demo"></div>
</div>
```
Now in order to conditionally attach a `css class` we need to bind the the `class` property. Notice that id doesn't matter that we've already attached a `class` here with the `demo`. With `:class` we are using VueJS syntax and we are not reusing the `class attribute`. Yes, we are binding to it, but behind the scenes VueJS will merge this all into one `class object`. In our `:class` we need to pass a JS `object` as an `argumnet`. And this `object` should be with a `css class` as a `key`, and as a `value` - should we attach or not.  

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <div class="demo" @click="attachRed = !attachRed" :class="{red: attachRed}"></div> <!--bind with class property-->
  <div class="demo"></div>
  <div class="demo"></div>
</div>
```

Now, when we click we attach our red block. We can turn on and off our class now with the click. 

![vue-with-css-classes2](../vue-with-css-classes2.png)
