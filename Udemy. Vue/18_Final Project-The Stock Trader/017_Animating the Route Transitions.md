# Animating the Route Transitions

To animate the `transitions` we need to go to our `App.vue` file where we have our `<router-view>` and wrap it in a `transition`. We can choose any name for the `animation`, let's choose "slide", and the `mode`. Now we go to the `<style>` and add classes: `.slide-enter-active` and  `.slide-leave-active`. These are the only two classes we need cos we are going to use `animations`. So, we'll setup some `keyframes` and after we setup `keyframes` we can use them in our classes. 

**App.vue**
```html
<template>
<div class="container">
        <app-header></app-header> 
        <div class="row">
            <div class="col-xs-12">
               <transition name="slide" mode="out-in">   <!--add a transition, animation, mode-->
                    <router-view></router-view>
                </transition>
        </div>
     </div>
 </div>
</template>

<script>
    import Header from './components/Header.vue'
    export default {
       components: {
           appHeader: Header
       },
       created(){
           this.$store.dispatch('initStocks');
       }
    }
</script>

<style>
body{
    padding: 30px;
}

.slide-enter-active {     /*add classes*/
  animation: slide-in 200ms ease-out forwards;
}

.slide-leave-active{
 animation: slide-out 200ms ease-out forwards;
}

@keyframes slide-in{        /*set keyframes*/
    from{
     transform: translateY(-30px);
     opacity: 0;
    }
    to{
     transform: translateY(0);
     opacity: 1;
    }
}

@keyframes slide-out {
    from{
     transform: translateY(0);
     opacity: 1;
    }
    to{
     transform: translateY(-30px);
     opacity: 0;
    }
} 
</style>
```