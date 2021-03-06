# Creating an Animation in Java Script

Now it's time to execute some code, so we could actually see animation. The place to animate is `enter` and `leave` functions. Let's say in `enter()` we wanna grow the width of our `div` and upon leaving make it smaller. For this we will setup a `variable` "round" here and then setup the `interval` cos we wanna grow it in steps, let's set the interval in 20 miliseconds, so every 20 miliseconds we will change our `div`. In the `function` inside the interval we execute the code we want to change every 20 miliseconds.  We access the element's width and grow the current width (we need to set it as a new property) with a round `el.style.width  = this.elementWidth (our current width) + round * 10`. As we wanna 100 pixels being the default, we need to set the new `property`, let's name it `elementWidth` and set it to 100, this will be our current width. Then of course we also need to increase `round` by one. And surely we need to set the `exit condition`: if `round` is greater than 20, if we executwd this 20 times let's say, then we wanna to clear interval with the `clearInterval()` method and call `done` here. We call `done()` here, cos we don't wanna mark that the whole `enter()` code has been executed, because we have asynchronous operation inside (`setInterval()`), then `done()` should be executed once we really done, once we reached our exit condition. 

For now it looks good, but we also need to set the initial width at `beforeEnter` hook, and then set the `element.style.width` to this width, so that we reset it to `100` before we enter it to the DOM, because if we added it before and removed it, this might have been in a different state, especially if we canselled some animation inbetween. 

With this setup we can go to `beforeLeave`,  here we wanna set the `element width` to 300 px. This is where it will be at the end after our `afterEnter` animation, and set the `element.style` width. Well, and for animating out we can simply copy the code from `enter()` and put it to `leave()`, the only thing we should change - decrease the width. Also we should change the width in our `div` in the template also to 300px. 

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Animations</h1>
                <hr>
                <select v-model="alertAnimation" class="form-control"> 
                <option value="fade">Fade</option>      
                <option value="slide">Slide</option>
                </select>
                <br><br>
                <button class="btn btn-primary" @click="show = !show">Show Alert!</button>
                <br><br>
                <transition :name="alertAnimation">  
                <div class="alert alert-info" v-if="show">This is some Info</div>
                </transition>
                <transition :name="alertAnimation" type="animation" appear>  
                <div class="alert alert-info" v-if="show">This is some Info</div>
                </transition>
                <transition  
                enter-active-class="animated bounce"   
                leave-active-class="animated shake"
                >  
                <div class="alert alert-info" v-if="show">This is some Info</div>
                </transition> 
                <transition :name="alertAnimation" mode="out-in" > 
                <div class="alert alert-info" v-if="show" key="info">This is some Info</div> 
                <div class="alert alert-warning" v-else key="warning">This is some Warning</div>  
                </transition> 
                <hr>
                <button class="btn btn-primary" @click="load = !load">Load / Remove Element</button> 
                <br><br>
                <transition @before-enter="beforeEnter" 
                @enter="enter"
                @after-enter="afterEnter"
                @enter-cancelled="enterCancelled"

                @before-leave="beforeLeave"
                @leave="leave"
                @after-leave="afterLeave"
                @leave-cancelled="leave-cancelled"
                :css="false"> 
                <div style="width: 300px; height: 100px; background-color: lightgreen" v-if="load"></div>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
             show: false,
             load: true,   
             alertAnimation: 'fade',
             elementWidth: 100         //set the new property
            }
        },
        methods:{         
            beforeEnter(el){
              console.log('beforeEnter');
              this.elementWidth = 100;     //reset the initial width
              el.style.width = this.elementWidth + 'px';  
            },
            enter(el, done){
              console.log('enter');
              let round = 1;   //set variable
              const interval = setInterval( ()=> {          //set interval
               el.style.width  = (this.elementWidth + round * 10) + 'px' //count width
               round ++     //increase round 
               if(round > 20){
                clearInterval(interval);
              done();
               }
              }, 20);
            },
            afterEnter(el){
              console.log('afterEnter')
            },
            enterCancelled(el){
                console.log('enterCancelled')
            },
            beforeLeave(el){
               console.log('beforeLeave');
              this.elementWidth = 300;  //set the final width 
              el.style.width = this.elementWidth + 'px'
            },
            leave(el, done){
               console.log('leave');
               let round = 1;   
              const interval = setInterval( ()=> {         
               el.style.width  = (this.elementWidth - round * 10) + 'px' //decrease the width
               round ++; 
               if(round > 20){
                clearInterval(interval);
                done();
               }
              }, 20);
            },
            afterLeave(el){
              console.log('afterLeave')
            },
            leaveCancelled(el){
             console.log('leaveCancelled')
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
transition: opacity 1s;   
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

![animation-in-js](../animation-in-js.png)
![animation-in-js2](../animation-in-js2.png)
