# Setting Up "Catch All" Routes / Wildcards

So, we want to be able to handle any `route` a user may enter which doesn't exist in our app. We can easily do this by adding one more `route` to `routes.js` file as the last `route`, which sholud catch everything that is not handeled by any of our other `routes`. And in this `route` we'll set up the `path` to be `*`, now if we redirect in such a case to just `/`, we can enter anything at the end of the URL after `/`, and it will be redirected to `Home` page, cos `*` start cathes it all. 

**routes.js**

```js
import User from './components/user/User.vue';
import UserStart from './components/user/UserStart.vue'  
import UserEdit from './components/user/UserEdit.vue';
import UserDetail from './components/user/UserDetail.vue';
import Home from './components/Home.vue';
import Header from './components/Header.vue';       

export const routes = [
{ path: '', name: 'home', components: { default: Home, 'header-top': Header } },     
{ path: '/user', components: { default: User, 'header-bottom': Header }, children: [    
{ path: '', component: UserStart },                    
{ path: ':id', component: UserDetail},                
{ path: ':id/edit', component: UserEdit, name: 'userEdit'}           
] },
{path: '/redirect-me', redirect: {name: 'userEdit'} },
{ path: '*', redirect: '/' }   //add a route that cathes all
];
```