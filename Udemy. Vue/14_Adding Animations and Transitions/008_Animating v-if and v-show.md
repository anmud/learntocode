# Animating `v-if` and `v-show`

Previously we used `v-if` in our `transition element`

```html
<transition name="fade">
 <div class="alert alert-info" v-if="show">This is some Info</div>
</transition>
 <transition name="slide" type="animation">  
 <div class="alert alert-info" v-if="show">This is some Info</div>
</transition>
```
We can easily change it to `v-show` and it will still work the same 

```html
<transition name="fade">
 <div class="alert alert-info" v-show="show">This is some Info</div> <!--change to v-show-->
</transition>
 <transition name="slide" type="animation">  
 <div class="alert alert-info" v-if="show">This is some Info</div>
</transition>
```

Though keep in mind `v-show` still doesn't remove or attach `elements` it only triggers the `display property`