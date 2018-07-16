# Using Namespaces to Avoid Naming Problems

If we are using multiple `modules` we have to be sure that we are not using the same name twice: all the `getters`, `actions` and `mutations` should have a unique name, and not only in the file they sit in, but in all the files that are finally get merged together in the main `store.js` file. For large applications there is a `pattern` we can use. We can create a new file in the `store` folder, let's name it `types.js`. And in this file we'll setup some `constants` that will get a `unique names`, which are all stored in this file, and which we'll then assign as names for our `methods` and `properties` and so on. 

**types.js**
```js
export const DOUBLE_COUNTER = 'counter/DOUBLE_COUNTER';
export const CLICK_COUNTER = 'counter/CLICK_COUNTER';

```

Now we can go to our `counter.js` file and here we need to import all the types from one `object`. And then due to ES6 we can use the syntax to setup a `dynamic property name`, by using squear brackets `[]` we can tell JS assign this `name` on runtime, so it then fetches the name from `types.js`, this will in the end be a string name. 

**counter.js**
```js
import * as types from '../types'     //import types here 

const state = {
    counter : 0
};

const getters = {                
    [types.DOUBLE_COUNTER]: state => {            //set the dynamic property name
              return state.counter * 2         
            },
    [types.CLICK_COUNTER]: state => {             //set the dynamic property name
                return state.counter + ' Clicks';
              },
};

const mutations = {
    increment: (state, payload) => {
           state.counter += payload;
        },
    decrement: (state, payload) => {
          state.counter -= payload;
       }
};

const actions = {               
    increment: ({ commit }, payload) => {
       commit('increment', payload);
     },
     decrement: ({commit}, payload) => {
       commit('decrement', payload)
     },
     asyncIncrement: ( {commit}, payload) => {         
       setTimeout (() => {
         commit('increment', payload.by);
     },payload.duration)
   },
     asyncDecrement: ({commit}, payload) => {         
       setTimeout (() => {
           commit('decrement', payload.by);
       },payload.duration)
     }
};

export default {
    state,
    getters,
    mutations,
    actions
}
```


Now with these names in place we also need to go to our `Result.vue` and `AnotherResult.vue` components. Here we also need to import `types.js`. Then in the `mapGetters` we need to pass an `object` instead of an `array` so we can still use our `names` here. And this allows us to use different names in our `template` and in our `getter`. 

**AnotherResult**
```html
<template>
<div>
    <p>Counter is: {{ doubleCounter }}</p>
    <p>Number of Clicks: {{ stringCounter }}</p>
</div>
</template>

<script>
    import { mapGetters } from 'vuex';
    import * as types from '../store/types';      //import types 

    export default {
       computed: {
          ...mapGetters({
              doubleCounter: types.DOUBLE_COUNTER,     //pass object with the names
              stringCounter: types.CLICK_COUNTER
          }) 
       }
    }
</script>
```

The same we have for the `Result.vue`component.

**Result.vue**
```html
<template>
    <p>Counter is: {{ counter }}</p>
</template>

<script>
    import { mapGetters } from 'vuex';
    import * as types from '../store/types'

    export default {
       computed: {
          ...mapGetters({
              counter: types.DOUBLE_COUNTER
          }) 
       }
    }
</script>
``` 
Now we are using `types.js` file to manage all our global names, and we ensure: 1. it's unique 2. the strings are unique, cos the strings are what the methods names at the end, cos we assign them dynamically, the strings are unique cos we prefixed them with the `module name` kind of.  