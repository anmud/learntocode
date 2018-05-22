# Dynamic Styling with CSS Classes: Using Objects

What if we don't want to store the `object` with a `class` in the html template? In our `vue instance` we can create a new `property` for that, which will depend on our `attachRed` property, so it need to be computed. This new `property` should return JS `object`. Ana=d in our html, we can simply replace our `object` with `divClasses`. 

**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <div class="demo" @click="attachRed = !attachRed" :class="divClasses"></div>  <!--replace the object with divClasses-->
  <div class="demo"></div>
  <div class="demo"></div>
</div>
```

**JS**

```js
new Vue ({
    el: '#app',
    data: {
    attachRed : false 
    },
    computed: {
    divClasses: function(){    //new property here 
     return {
         red: this.attachRed,   
         blue: !this.attachRed
     }
    }
    }
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
.red {                      
background-color: red;
}
.green {                   
background-color: red;
}
.blue {                 
background-color: red;
}
```