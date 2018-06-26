# Setting Up an Initial (on-load) Animation

Let's say we have three elements and generally set `show` in the `data object` to true. Let's say we wanna animate the third element when the page is loaded first. To tell VueJS to animate the initial attaching to the DOM, we cann add the `appear attribute` to the `transition element`. 

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
                <transition name="slide" type="animation">  
                <div class="alert alert-info" v-if="show">This is some Info</div>
                </transition>
                <transition name="fade" appear>   <!--add appear attribute-->
                <div class="alert alert-info" v-if="show">This is some Info</div>
                </transition>  <!--add one more element-->
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
             show: true    //set show to true
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
opacity: 0;          
}

.slide-eneter-active{
animation: slide-in 1s ease-out forwards;  
transition: opacity .5s;         
}

.slide-leave{

}

.slide-leave-active{
animation: slide-out 1s ease-out forwards;
transition: opacity 3s;   
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