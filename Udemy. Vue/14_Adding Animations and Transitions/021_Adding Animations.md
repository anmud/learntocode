# Adding Animations

Well, the application is working, but it's not beutiful though. Let's use animation. 
In `App.vue` we'll wrap our `component` in a `transition` and then for this `transition` we wanna setup the `name`, and the name is `flip` cos we wanna flip this; and we'll set the `mode` to `out-in` so that the old component was first removed before the new one is animated in. Since we add `flip` we need to add `css classes` in the `style` part. Since we wanna `flip` we also need `keyframes` with animation to do that. Which animations we wanna setup here? For `flip-out` we wanna `transform`, and `rotateY` (so we rotate around the Y axis), and initially we wanna to rotate this by `0` degrees, because we will start with having it not rotated at all; but we wanna transform to `rotateY()` on 90 degrees. Then for `flip-in` we have to start at the point where the first `component` stops and we wanna to transform it to `0` degrees again. 

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1 class="text-center">The Super Quiz</h1>
            </div>
        </div>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3"> 
            <transition name="flip" mode="out-in">  <!--wrap in transition-->
                <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question' "></component> 
            </transition> 
            </div>
        </div>
        
    </div>
</template>

<script>
    import Question from './components/Question.vue';
    import Answer from './components/Answer.vue';

    export default {
        data: function(){
         return{
         mode: 'app-question'     
         }
        },
        methods:{
        answered(isCorrect) {
              if (isCorrect) {
                  this.mode = 'app-answer';
              } else {
                  this.mode = 'app-question';
                  alert('Wrong, try again!');
              }
          }
        },
        components:{
            appQuestion: Question,
            appAnswer: Answer
        }
    }
</script>

<style>   /*add classes here*/

.flip-enter{
/*transform : rotateY(0deg)*/
}
.flip-enter-active{
animation: flip-in 0.5s ease-out forwards;
}

.flip-leave{
/*transform: rotateY(0deg)*/
}

.flip-leave-active{
animation: flip-out 0.5s ease-out forwards;
}

@keyframes flip-out{    /*set keyframes*/
    from{
    trasform: rotateY(0deg);
    }
    to{
    transform: rotateY(90deg)
    }
}

@keyframes flip-in{
    from{
    trasform: rotateY(90deg);
    }
    to{
    trasform: rotateY(0deg); 
    }
}
</style>
```

After that let's setup `css classes`. At `flip-enter` should be `transform : rotateY(0deg)`, but actually we don't need to set this, cos this is the starting state. `flip-enter-active` should use the `flip-in` animation over let's say half a second. For `flip-leave` we also wanna `transform rotateY()` - we also comment this out. And for `flip-leave-active` we wanna have our animation, where we play `flip-out` over half a second. 