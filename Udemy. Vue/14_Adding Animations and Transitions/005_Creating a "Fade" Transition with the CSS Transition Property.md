# Creating a "Fade" Transition with the CSS Transition Property

Now we wanna fade our `alert` in and out. To do that in our `<style>` part we'll use a `fade-enter` css class. Remember that here we should set our initial state we want to have. Since we wanna fade it in it should initially be transparent, therefore we will set the `opacity` to zero and this is it. We wouldn't set any `transition` here, cos remember this class will immediately be removed after one frame. The place to set up a `transition` is in `fade-enter-active` class. Here we would transition our `opacity` over 1 second. For leaving we could set `opacity` to `1` (in `fade-leave` class), but we shouldn't cos this is default. For `fade-leave-active` though we again should setup the `transition`, and here is important to set up the `opacity` to `0`. Remember the default already is `1`, that's why we set both the `transition` and the `opacity` to `0`, we tell it "yes, animate it whenever the opacity changes, and look here it changes to `0`". 

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Animations</h1>
                <hr>
                <button class="btn btn-primary" @click="show = !show">Show Alert!</button>
                <br><br>
                <transition name="fade">
                <div class="alert alert-info" v-if="show">This is some Info</div>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
             show: false
            }
        }
    }
</script>

<style>
.fade-enter{        /*set initial state here*/
 opacity: 0;
}
.fade-enter-active{
transition: opacity 1s;            /*set transition here*/
}
.fade-leave{
/*opacity:1 - is the default state*/

}
.fade-leave-active{
    transition: opacity 1s;           /*set transition here*/
    opacity: 0;              /*set opacity to 0 here*/
}
</style>
```

Now VueJS is able to sniff these `CSS classes`, finds out that the `transition length` is 1 second, and it does the same for the leaving. 