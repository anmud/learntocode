# Using Separate Files
Sometimes we can have `state`, `getters` some `actions`,  which don't belong into one module. In the application let's say we have a `users part` and the `blog part` and that would be two great `modules`. But then also we have some `state` which is only displayed in the `header`, which has to be everywhere. Therefore we don't want to put the `header related state` into either of two `modules`. We can leave it in our main `store.js` file, but it could be overloaded as well. To fix this task it would be great to cteate other files: `actions.js`, `getters.js`, `mutations.js` in the `store folder`. 

![separate-files](./separate-files.png)

Now we can take our `action` from `store.js` file and in the `actions.js` file we'll export a `constant`, name it with the name of the `action` and this is of course a `function`. And if we have more `actions` we simply will add more `export const`. 

**actions.js**

```js
export const  updateValue = ({commit}, payload) => {         //create const for an action    
    commit('updateValue', payload);
};
```

Now in our `store.js` we surely need to import our newly created `actions.js` file. Here we'll use the `star syntax` - `* as actions` - to let JS create an `object`, which we can access with the name "actions", this is the `object` where our all `exported const` are basically just properties. So with that we can just use (like register)`actions` in the script. We can do the same with `mutations` and `getters`. 

**store.js**
```js
import Vue from 'vue';          
import Vuex from 'vuex';
import counter from './modules/counter';
import * as actions from './actions';   //import actions.js here 
import * as mutations from './mutations';   //import mutations.js here 
import * as getters from './getters';         //import getters.js here 


Vue.use(Vuex);  

export const store = new Vuex.Store({                
    state: {
         value: 0
    },
    getters,     //use getters tions here 
    mutations,   //use mutations here 
    actions,        //use actions here 
    modules:{
         counter
       }       
});     
```

Of course, we could split also our `modules` for `actions`, `getters` and `mutations`. 