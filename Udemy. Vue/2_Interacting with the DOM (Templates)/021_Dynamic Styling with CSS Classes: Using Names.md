# Dynamic Styling with CSS Classes: Using Names

Sometimes, we don't want to decide if a certain `class` should be attached or not, but we wanna calculate or dynamically derive which `class` should be attached or not. 

### Example 

Let's add an `input` field and bind it to our `color` property. Initialy we set our `color property` to green, reffering ot the `css class`. In our html we bind our `div` to `css classes` with `:class` and set it equal to `color` property.


**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <div class="demo" @click="attachRed = !attachRed" :class="divClasses"></div>  
  <div class="demo"></div>
  <div class="demo" :class="color"></div>
  <hr>
  <input type="text" v-model="color"
</div>
```

**JS**

```js
new Vue ({
    el: '#app',
    data: {
    attachRed : false,
    color: "green"  // color property here 
    },
    computed: {
    divClasses: function(){   
     return {
         red: this.attachRed,   
         blue: !this.attachRed
     }
    }
    }
});
```

Now if we enter "green" to our `input` the block will be green, the same way we can change it to "blue" for example - just type it in the `input`. We can also attach multiple classes by using the `array` syntax - `[color]`.
We can ad an `obect` as a second argument `:class="[color, {red: attachRed}]"`. Now we get a mixture - and if we don't type the color in the `input` we have our block to be `red`. Becuase we set an `array` of classes which we wanna VueJS to analyse and then merge it all into one list of `css classes`, based on whatever the `items` in the `array` resolve to. And they resolve to `color` property  - which is a `css class` ('green' - is the `name` of `css class`) and to an `object`. If it's an `object` then VueJS knows: ok, it's a `key value pair`, where the `key` is a `css class` and the `value` is the condition if this `class` should be attached or not. 

So, we have both syntaxes - using the `css class` directly, or using an `object` where then the `key` is a `css class` and the `value` is the condition.  


**HTML**

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>

<div id="app">
  <div class="demo" @click="attachRed = !attachRed" :class="divClasses"></div>  
  <div class="demo"></div>
  <div class="demo" :class="[color, {red: attachRed}]"></div> 
  <hr>
  <input type="text" v-model="color"
</div>
```