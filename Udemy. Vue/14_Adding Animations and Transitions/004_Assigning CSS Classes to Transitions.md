# Assigning CSS Classes to Transitions

Well, to animate our `element`, using `transitions`, in our `App.vue` template, we set the `name` attribute for the `transition` and name it "fade". This means VueJS now attaches `-enter`, `*-enter-active`, `-leave` and `leave-active`. Now we can setup `classes` in our `<style>` section of code. Important to keep in mind that VueJS will analyse this code and therefore determines how long the animation runs. 

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
                <transition name="fade">        <!--set name attribute-->
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

}
.fade-enter-active{

}
.fade-leave{

}
.fade-leave-active{
    
}
</style>
```
