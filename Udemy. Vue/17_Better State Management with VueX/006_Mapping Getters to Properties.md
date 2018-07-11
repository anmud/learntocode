# Mapping Getters to Properties

What is we want to have another `getter`? So, in our `getters` property in the `store` we'll have "stringCounter" property, let's name it this way, where we taka our `state` and return our `state.counter + 'Clicks'` to turn it to a string. 

**store.js**

```js
import Vue from 'vue';          
import VueX from 'vuex';

Vue.use(VueX);  

export const store = new VueX.Store({              
    state: {
         counter: 0           
},
    getters: {                  
        doubleCounter: state =>{
       return state.counter * 2         
     },
       stringCounter: state => {             //set one more getter
         return state.counter + 'Clicks';
       }

    }
});            
```

Let's use this new `getter` in the `AnotherResult.vue` component. Here we'll have one more `paragraph` where we output our `"clicks" computed property`, which we'll create in the script and then return 

**AnotherResult**

```html
<template>
<div>
    <p>Counter is: {{ counter }}</p>
    <p>Number of clicks: {{ clicks }}</p>        <!--output number of clicks-->
</div>
</template>

<script>
    export default {
       computed: {
            counter() {
              return this.$store.getters.doubleCounter;     
            },
            clicks (){
                return this.$store.getters.stringCounter;     //create computed property
            }
        }
    }
</script>
```