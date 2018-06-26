# Creating a "Slide" Transition with CSS Animation Property

Let's now use `animation` instead of `transition`. Let's say we wanna slide our `alert`. We need to setup `slide-enter`, `slide-eneter-active`, `slide-leave`, `slide-leave-active` classes. 

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

.slide-enter{             /*set slide classes here*/

}

.slide-eneter-active{

}

.slide-leave{

}

.slide-leave-active{

}
</style>
```

Now we could use these `classes` by setting up the `name` of the class in the `template`. And for animations to be available we also need to add `keyframes` and in there we will have a `slide-in` and `slide-out` animation. Inside the `keyframes` we should specify the individual percentages (from and to). We wanna start with sliding it in with `transform`, so we wanna move it in it's position with `translateY()` on the Y axis, and then we wanna move it 20 px. And then `to` - is where we wanna end, and we wanna end at the real position of the `element`. We da the same for the `slide-out` animation but with the opposite place on the axis. 

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
                <transition name="slide">  <!--setup the name of a class-->
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

}

.slide-eneter-active{

}

.slide-leave{

}

.slide-leave-active{

}

@keyframes slide-in{         /*set keyframes */
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

With the `keyframes` setup we can set the slide classes. Since we setup the starting state in the `keyframes` we shouldn't set up this on the `slide-enter` class. In `slide-enter-active` we now wanna play this animation - so the animation should be `slide-in` referring to our `slode-in keyframes`, do it in `1` second, use `ease-out` function to end a bit slower that we start, and important we need to setup `forwards` so that the `element` stays at the finishing position of the animation and doesn't snap back. For the leave we will not need to have the initioa state, cos the starting position of the `element` is the default position of the `element`. For `slide-leave-active` we will use `slide out keyframe`. 

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
                <transition name="slide">  <!--setup the name of a class-->
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
/* transform: translateY(20px)*/
}

.slide-eneter-active{
animation: slide-in 1s ease-out forwards;  /* play animation*/
}

.slide-leave{

}

.slide-leave-active{
animation: slide-out 1s ease-out forwards;
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
