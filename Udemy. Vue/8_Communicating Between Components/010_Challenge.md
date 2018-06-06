# Challenge

1. In `Servers` component we need a separate `component` for each `list item`, and we `loop` through these separate components we created. 
2. Pass the current index (server number) to the each server in the list. 
3. Create an `array` of `server objects` in `Server.vue` component. Then pass the id of each server to each component of the list item. 
4. Whwen we click a server in the list, we wanna load it in the `serverDetails` component. In `ServerDetails` we have a `button` to switch the server `status`, which should always be managed in a `data` property of the `Servers.vue` object. 

### Solution

**Servers.vue**

```html
<template>
<div class="col-xs-12 col-sm-6">
<ul class="list-group">
<app-server v-for="server in servers" :server="server"></app-server> 


</ul>
</div> 
</template>

<script>
import Server from './Server.vue';

export default {

data: function(){
return {
servers: [
{id: 1, status: 'Normal'},
{id: 2, status: 'Critical'},
{id: 3, status: 'Unknown'},
{id: 4, status: 'Normal'},
{id: 5, status: 'Critical'}
]
};
},
components: {
'app-server': Server
}
}

</script>

<style>
</style>
```

**Server.vue**

```html
<template>

<li class="list-group-item" style="cursor:pointer" @click="serverSelected">
Server # {{ server.id }}

</li>

</template>

<script>
import {serverBus} from '../main'
export default {
props: ['server'],
methods:{
serverSelected(){
serverBus.$emit('serverSelected', this.server)
}
}
}

</script>

<style>
</style>
```

**ServerDetails.vue**

```html
<template>
<div class="col-xs-12 col-sm-6">
<p v-if="!server">Please select a server</p>
<p v-else>Server number # {{server.id}} selected, status: {{server.status}}</p>
<hr>
<button @click="resetStatus">Change to Normal</button>
</div>
</template>

<script>
import {serverBus} from '../main'

export default {
data: function(){
return{
server: null
}
},
methods:{
resetStatus (){
this.server.status = "Normal";
}
},
created(){
serverBus.$on('serverSelected', (server)=>{
this.server = server; 
});
}
}

</script>

<style>
</style>
```

**main.js**

```js
import Vue from 'vue'
import App from './App.vue'

export const serverBus = new Vue();

new Vue({
el: '#app',
render: h => h(App)
})
```

