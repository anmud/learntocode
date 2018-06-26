# Mixing Transition and Animation Properties

Let's mix now `transitions` and `animation`. Let's adjust our sliding animation, so that it's no just sliding up and down but it is also becoming transparent. To achieve this we will first adjust our `.slide-enter` class, here we will have the initial `opacity` of `0`. In the `slide-enter-active` we aslo need a `transition`, where we set the `opacity` over `half a seond`, let's say. In the `slide-leave-active` we need to set up the `transition` for leaving, and here we will animate the opacity for one second let's say, and of course set the `opacity` to `0` here. 

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
                <transition name="slide" type="animation">  <!--set the type-->
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
.fade-enter{        
 opacity: 0;
}
.fade-enter-active{
transition: opacity 1s;           
}
.fade-leave{

}
.fade-leave-active{
    transition: opacity 1s;          
    opacity: 0;             
}

.slide-enter{           
opacity: 0;          /*set opacity*/
}

.slide-eneter-active{
animation: slide-in 1s ease-out forwards;  
transition: opacity .5s;         /*set transition*/
}

.slide-leave{

}

.slide-leave-active{
animation: slide-out 1s ease-out forwards;
transition: opacity 3s;   /*set transition for leaving*/
opacity: 0;
}

@keyframes slide-in{        
 from{
 transform: translateY(20px);
 }
 to{
 transform: translateY(0);
 }
}

@keyframes slide-out{
 from{
 transform: translateY(0);
 }
 to{
 transform: translateY(20px);
 }
}
</style>
```

Though, we do have a problem here now, since we have both `animation` and `transition` here VueJS doesn't know which one to use, in casee we have two different durations here VueJS takes the longer one. We can tell VueJS which `duration` of which `property` to use by adding a `type property` in the template to the `transition` component, and then setting the type either to `animation` or the `transition`, because these are two css properties we can use to animate things, and with that we can set up which one to use. So we will set the slide as `animation` type and this will make sure that for VueJS `animation` finishes. So, the removing of the `element` is done once the `animation` finishes. 