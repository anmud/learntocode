# Using an Event Bus for Communication

The third way for sibling communication is using central `object` to pass the `data`. 
Well, to use it we'll create a new `vue instance` in our `main.js` file, and store it in a constant which we export. 

**main.js**

```js
import Vue from 'vue'
import App from './App.vue'

export const eventBus new Vue(); //new vue instance

new Vue({
  el: '#app',
  render: h => h(App)
})
```
So, with this object setup we can go to our `UserEdit` component and there we wanna import this new object. And call `$emit` method for our `eventBus`. Important!!!! This is emitted on the `eventBus` instance. 

**UserEdit**

```html
<template>
    <div class="component">
        <h3>You may edit the User here</h3>
        <p>Edit me!</p>
        <p>User Age: {{userAge}}</p>
        <button @click="editAge">Edit Age</button>
    </div>
</template>

<script>
import {eventBus} from '../main.js';   //import eventBus 
export default{
 props: ['userAge'],
 methods:{
     editAge(){
         this.userAge = '30';
         eventBus.$emit('ageWasEdited', this.userAge)    //emit on eventBus instance
     }
 }
}
</script>

<style scoped>
    div {
        background-color: lightgreen;
    }
</style>
```
Well, since it is a separate instance we can go to our `UserDetail` component and add a new lifecycle hook, `created()`. We wanna use this hook, cos we wanna setup a listner to this `event`. This `listner` should keep running from the beginning of this `component` on. For that we import new `vue instance` for the `UserDetail` component too. This `created()` will listen to the `vue instance` we created and stored in the `evenBus` in `main.js`. So inside we wanna listen to the 'ageWasEdited' event because this is the name we chose in the `UserEdit` component, and we know that it get some `data`. This `data` is always used as a second `argument`, which is always a callback function which should get executed whenever such an event occurs. This callback always gets the `data` we pass with the `event`, passed as an `argument`. 

**UserDetail**
```html
<template>
    <div class="component">
        <h3>You may view the User Details here</h3>
        <p>Many Details</p>
        <p>User Name: {{switchName()}}</p>
        <p>User Age: {{userAge}}</p>
        <button @click="resetName">Reset the Name</button>
         <button @click="resetFn()">Reset the Name</button>
    </div>
</template>

<script>
import {eventBus} from '../main.js';      //import new vue instance
export default {
    props: {
        name: {
            type: String
            },
        resetFn: Function,
        userAge: Number  
            },
    methods: {
     switchName(){
      return this.name.split('').reverse().join('');
     },
     resetName(){
         this.name = "Max";
         this.$emit('nameWasReset', this.name)
     },
     created(){               //lifecycle hook 
      eventBus.$on('ageWasEdited', (age)=>{     //callback
       this.userAge = age;
      });
     }
    }
}
</script>

<style scoped>
    div {
        background-color: lightcoral;
    }
</style>
```

However, in the `main.js` 