# Where the "resource" in vue-resource comes from

`Vue-resource` has a nice extra feature, which allows us to set our own resourses, which are kind of mappings of common tasks to `http requests`. For example, we wanna store smth in a `data base`, typically it would make sense if it would call a `save` method on our `data` and then that would automatically send a `post request` to the right URL with the `data` attached to it. Now, the resources we can setup with `vue-resource` allow us to do that. 

Let's go to the `App.vue` file. The first thing we need to do, is to create such `resourses`, for that we;ll have a new key in our `data object` and this will be just an empty object. Then we'll setup the `created()` lifecycle hook, cos that is a good place to initialise resourses. Then we can set it up by using our `resource` property we just created and then accessing `this.$resource` - this is actually a `method`. To this method we have to pass certain `data fields`: the first field is the resource, that could be `data.json`, this will again use our `root URL` we setup earlier in `main.js` file. As we already have in our URL `data.json` - for now we'll remove it from the `root URL` in our `main.js`. Then in the `App.vue` we'll use `data.json` as the first argument. 

**App.vue**
```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Http</h1>
                <div class="form-group">          
                <label>User Name</label> 
                <input class="form-control" type="text" v-model="user.username"> 
                </div>
                <div class="form-group">          
                <label>Mail</label> 
                <input class="form-control" type="text" v-model="user.email"> 
                </div>
                <button class="btn btn-primary" @click="submit">Submit</button>   
                <hr>
                <button class="btn btn-primary" @click="fetchData">Get Data</button>  
                <ul class="list-group">
                <li class="list-group-item" v-for="(u, index) in users" :key="index">{{u.username}} - {{u.email}}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
            return{
                user:{
                    username: '',
                    email: ''
                },
                users: [],
                resource: {}         //create resourses here 
            };
        },
        methods:{              
            submit(){
                this.$http.post('data.json', this.user) //use as the first argument
                .then(response => {       
                 console.log(response)
                }, error =>{
                 console.log(error)
                });
            },
            fetchData(){       
             this.$http.get('data.json')   //use as the first argument
             .then(response =>{         
              return response.json(); 
             })
             .then(data =>{
              const resultArray = [];
              for(let key in data){
              resultArray.push(data[key])
              }
              this.users = resultArray;
             });
            },
            created(){                 //set resource here
                this.resource = this.$resource('data.json')
            }
        }
    }
</script>

<style>
</style>
```

**main.js**
```js
import Vue from 'vue'
import VueResource from 'vue-resource'; 
import App from './App.vue'

Vue.use(VueResource); 

Vue.http.options.root = 'https://vuejs-http-baec0.firebaseio.com/'      //remove data.json from url

Vue.http.interceptors.push( (request, next) => {
    console.log(request);
    if(request.method == 'POST'){
     request.method = 'PUT'
    }
    next( response => {
     response.json = () => {
     return { messages: response.body }
     }
    });
});

new Vue({
  el: '#app',
  render: h => h(App)
})
```

Let's use the `resource` we just created. 