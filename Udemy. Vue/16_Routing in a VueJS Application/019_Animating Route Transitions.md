# Animating Route Transitions

If we have a look at our `router` in the `App.vue` file, we can simply wrap `<router-view>` with the `<transition>` component, because it is only one element, to transition group here; only one element, because we want to `transition` between the `components` which get loaded in this `router-view`. This will now `transition` or `animate` the switching of these `routes`. We can set a simle animation using `slide` animation for example, and setup this in the `style` section. And then set the `mode` to `out-in` so that the first component removed before the new one is added. 

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Routing</h1>
                <hr>
                <router-view name="header-top"></router-view> 
                <transition name="slide" mode="out-in">       <!--wrap in transition, setup animation-->
                <router-view></router-view>
                </transition>
                <router-view name="header-bottom"></router-view>
            </div>
        </div>
    </div>
</template>

<script>
    import Header from './components/Header.vue'
    export default {
        components:{
            appHeader: Header
        }
    }
</script>

<style>
   .slide-leave-active {
        transition: opacity 1s ease;
        opacity: 0;
        animation: slide-out 1s ease-out forwards;
    }

    .slide-leave {
        opacity: 1;
        transform: translateX(0);
    }

    .slide-enter-active {
        animation: slide-in 1s ease-out forwards;
    }

    @keyframes slide-out {
        0% {
            transform: translateY(0);
        }
        100% {
            transform: translateY(-30px);
        }
    }

    @keyframes slide-in {
        0% {
            transform: translateY(-30px);
        }
        100% {
            transform: translateY(0);
        }
    }
</style>
```
Well, important thing here is - wrap the `router-view` for which we want to animate with `transition` and then setup the `transition` as we know already: with name, classes, possibly with js hooks, with the mode and so on.