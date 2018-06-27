# Configuring vue-resource Globally

It would be great to have a global place to set for each `http request` and not to repeat this code with the URL. Well, we have such a central place where we can setup our application URL. In our `main.js` where we setup our `vue-resource`, after this we can call `Vue.http` and IMPORTANT without dollar sign `$`, and here we can setup some global options. To know more about these `global options` dive into official Vue-resource documentation, there we will find [API docs](https://github.com/pagekit/vue-resource/blob/develop/docs/api.md)where we can learn more about which `options` we can setup. 

In our example we got the access to the `root key` of the global options, and the `root key` is basically our main URL we are going to use. After setting up this, all request will be sent to this URL.

**main.js**
```js
import Vue from 'vue'
import VueResource from 'vue-resource'; 
import App from './App.vue'

Vue.use(VueResource); 

Vue.http.options.root = 'https://vuejs-http-baec0.firebaseio.com/data.json'      //configure globally 

new Vue({
  el: '#app',
  render: h => h(App)
})
```

And then in our `methods` in `App.vue` file we can simply append things to this URL, e.g if we cover everything we need like in our example, we can have just empty string. 

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
                <button class="btn btn-primary" @click="fetchData">Get Data</button>  <!--new button here-->
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
                users: []
            };
        },
        methods:{              
            submit(){
                this.$http.post('', this.user) //empty string because of global setting
                .then(response => {       
                 console.log(response)
                }, error =>{
                 console.log(error)
                });
            },
            fetchData(){       
             this.$http.get('')  //empty string because of global setting
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
            }
        }
    }
</script>

<style>
</style>
```