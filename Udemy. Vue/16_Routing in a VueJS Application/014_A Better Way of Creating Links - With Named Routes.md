# A Better Way of Creating Links - With Named Routes

`Vue-router` offers a better way of creating `link` for the `path`. We can give our `routes` names. In our `routes.js` file we can assign a name to the routes, we can choose any name we want.

**routes.js**

```js
import User from './components/user/User.vue';
import UserStart from './components/user/UserStart.vue'  
import UserEdit from './components/user/UserEdit.vue';
import UserDetail from './components/user/UserDetail.vue';
import Home from './components/Home.vue';

export const routes = [
{ path: '', component: Home },
{ path: '/user', component: User, children: [         
{ path: '', component: UserStart },                    
{ path: ':id', component: UserDetail},                
{ path: ':id/edit', component: UserEdit, name: 'userEdit'}   //add a name to the route            
] }    
];
```

Now, when we added a `name` to the route, we can identify this `route` by name, which means that on any page whenever we'll setup the link, for example in our case in `userDetali`, we can now pass on `object` insteand of a `string`. And in this object we get a couple of `properties` to define which `path` we want to navigate to. 

**UserDetail**

```html
<template>
<div>
    <h3>Some User Details</h3>
    <p>User loaded has ID: {{ $route.params.id }}</p>
    <router-link tag="button" :to="{name='userEdit'}" class="btn btn-primary">Edit User</router-link>  <!--navigate to edit-->
</div>
</template>
```

Now VueJs will automatically populate the real `path` with the `path` that extracts from the `name` of the route, we don't need to type the full `path`; then we can pass the second `argument` - `params` which is again an `object`, where we can now pass `key-value pairs` of the `parameters` we want to pass to this `path`. 

**UserDetail**

```html
<template>
<div>
    <h3>Some User Details</h3>
    <p>User loaded has ID: {{ $route.params.id }}</p>
    <router-link tag="button" :to="{name='userEdit', params: {id: $route.params.id}}" class="btn btn-primary">Edit User</router-link>  <!--add a second parameter-->
</div>
</template>
```

Important thing here is - we can use this setup in any `router-link` always pass an `object` to `to=` to set the `path`. And it is the same `object` we can pass to, when having our `router` in code, like we have in our case in `User.vue` file, when we push the `path` in the methods. 

**User.vue**

```html
<template>
    <div>
        <h1>The User Page</h1>
         <p>Loaded ID: {{ id }}</p>  
         <button class="btn btn-primary" @click="navigateToHome">Go to Home</button>
    </div>

</template>

<script>
export default{       
    methods:{
        navigateToHome(){
        this.$router.push('/')  //we push path 
        }
        
    }
}
</script>
```

Here when we push the `path` we could also pass an `object` and setup the `path`. 

**User.vue**

```html
<template>
    <div>
        <h1>The User Page</h1>
         <p>Loaded ID: {{ id }}</p>  
         <button class="btn btn-primary" @click="navigateToHome">Go to Home</button>
    </div>

</template>

<script>
export default{       
    methods:{
        navigateToHome(){
        this.$router.push( {path: '/'} )  //we setup path 
        }
        
    }
}
</script>
```

Or also use a `name route`. 

**User.vue**

```html
<template>
    <div>
        <h1>The User Page</h1>
         <p>Loaded ID: {{ id }}</p>  
         <button class="btn btn-primary" @click="navigateToHome">Go to Home</button>
    </div>

</template>

<script>
export default{       
    methods:{
        navigateToHome(){
        this.$router.push( {name: 'home'} )  //we use name route 
        }
        
    }
}
</script>
```


