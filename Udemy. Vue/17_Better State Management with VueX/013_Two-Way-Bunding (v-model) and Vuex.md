# Two-Way-Bunding (v-model) and Vuex

Let's look at one important case. Imagine in our `store.js` we not only get the `counter` but we also got the `value`, the glabal `value` which is `0` initialy. This `value` should be set in any of our `components`, so for that we need to set the `getter` let's name it "value", and here we get our `state` and we simply want to return `state.value`. And we need to create a `mutation` for it, which we;ll name "updateValue", which get the `state` and the `payload`, and set `state.value = payload` so the `new payload` is just a number that then should be a `new value`. Then we'll setup an `action` for this, it's also called "updateValue". 

**store.js**
```js
import Vue from 'vue';          
import Vuex from 'vuex';

Vue.use(Vuex);  

export const store = new Vuex.Store({                
    state: {
         counter: 0,
         value: 0             //we got value here 
    },
    getters: {                
            doubleCounter: state => {
              return state.counter * 2         
            },
            stringCounter: state => {             
                return state.counter + ' Clicks';
              },
            value: state => {                //set the value getter
               return state.value; 
            }
           },
           mutations: {
            increment: (state, payload) => {    
               state.counter += payload;       
            },
            decrement: (state, payload) => {
              state.counter -= payload;
           },
           updateValue: (state, payload) =>{         //set the value mutation
               state.value = payload
           }
         },
         actions:  {                   
            increment: ({commit}, payload) => {     
              commit('increment', payload);
            },
            decrement: ({commit}, payload) => {
              commit('decrement', payload);
            },
            asyncIncrement: ({commit}, payload) =>{         
              setTimeout ( () => {
                  commit('increment', payload.by);        
              },payload.duration)                       
            },
            asyncDecrement: ({commit}, payload) =>{         
              setTimeout ( () => {
                  commit('decrement', payload.by);
              },payload.duration)
            },
            updateValue: ({commit}, payload)=>{        //set the value action
                commit('updateValue', payload);
            }
         }      
});     
```

In the `App.vue` we wanna add an `input` which should allow us to set `the value`. First we need to setup a `computed property`, we'll name it "value", where we want to return `this.$store.getters.value` - the name of the `getter` we created before in our `store.js`. And now if in the `input` we bind `value="value"` 

**App.vue**
```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Vuex</h1>
                <app-result></app-result>
                <app-another-result></app-another-result>
                <hr>
                <app-counter></app-counter>
                <app-another-counter></app-another-counter>
                <hr>
                <input type="text" :value="value">      <!--create input here-->
            </div>
        </div>
    </div>
</template>

<script>
    import Counter from './components/Counter.vue';
    import AnotherCounter from './components/AnotherCounter.vue';
    import Result from './components/Result.vue';
    import AnotherResult from './components/AnotherResult.vue';


    export default {
        computed: {                      //set computed value here
            value(){
                return this.$store.getters.value
            }
        },
        components: {
            appCounter: Counter,
            appResult: Result,
            appAnotherResult: AnotherResult,
            appAnotherCounter: AnotherCounter
        }
    }
</script>
```

We see it works.  ![v-model-vuex](./v-model-vuex.png)

But what issue we got there? Well, let's say we not only want to display the `value` but set it. This way `v-model="value"` will not work, because `value` is a `computed property` not a normal `property`. The `value` will stay the same, because the `state` in our `store` hasn't been touched, because our `computed value` is only a `getter`, we can't set it with two-way binding (v-model). 

Well, here is one way we could fix it: for this we'll setup a `method` which we'll call `updateValue`, where we call `this.$store.dispatch('updateValue')`, and pass `event.target.value` as the second argument. And now add an `input event` to the `input` and execute `updateValue` on it. 

**App.vue**
```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Vuex</h1>
                <app-result></app-result>
                <app-another-result></app-another-result>
                <hr>
                <app-counter></app-counter>
                <app-another-counter></app-another-counter>
                <hr>
                <input type="text" :value="value" @input="updateValue">      <!--create input here-->
                <p>{{ value }}</p>
            </div>
        </div>
    </div>
</template>

<script>
    import Counter from './components/Counter.vue';
    import AnotherCounter from './components/AnotherCounter.vue';
    import Result from './components/Result.vue';
    import AnotherResult from './components/AnotherResult.vue';


    export default {
        computed: {                      
            value(){
                return this.$store.getters.value
            }
        },
        methods:{                        //create method here
         updateValue (event){
             this.$store.dispatch('updateValue', event.target.value)
         }
        },
        components: {
            appCounter: Counter,
            appResult: Result,
            appAnotherResult: AnotherResult,
            appAnotherCounter: AnotherCounter
        }
    }
</script>
```
Now, if we enter something in the `input` the `state` gets updated as well.

![v-model-vuex2](./v-model-vuex2.png)

But the problem here is we setup our so to say "custom" `two-way-binding`. What if we really want to use the shorter way of `v-model="value"`? We can do this by changing our `computed property`. Actually we can for the `computed propertiies` setup a `getter` and a `setter`. We can turn our `computed property` into an object where we'll have a `get()` and a `set()` methods; the `get` is responsible for getting the `value` and  the `set` gets the `value` as an argument, and we can use the `value`. This way we can use `v-model` for our `input`. Still, keep in mind this is a very rare option, where we can use `get` and `set` in the `computed property`.

**App.vue**
```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Vuex</h1>
                <app-result></app-result>
                <app-another-result></app-another-result>
                <hr>
                <app-counter></app-counter>
                <app-another-counter></app-another-counter>
                <hr>
                <input type="text" v-model="value" @input="updateValue">     <!--use v-model-->
                <p>{{ value }}</p>
            </div>
        </div>
    </div>
</template>

<script>
    import Counter from './components/Counter.vue';
    import AnotherCounter from './components/AnotherCounter.vue';
    import Result from './components/Result.vue';
    import AnotherResult from './components/AnotherResult.vue';


    export default {
        computed: {                      
            value: {                //transform the computed property
                get (){              //use get method
                return this.$store.getters.value
                },
                set(value){            //use set method
                 this.store.dispatch('updateValue', value)
                }
            }
        },
        methods:{                       
         updateValue (event){
             this.$store.dispatch('updateValue', event.target.value)
         }
        },
        components: {
            appCounter: Counter,
            appResult: Result,
            appAnotherResult: AnotherResult,
            appAnotherCounter: AnotherCounter
        }
    }
</script>
```