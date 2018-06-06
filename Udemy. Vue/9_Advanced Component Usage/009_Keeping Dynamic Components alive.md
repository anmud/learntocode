# Keeping Dynamic Components alive

Inoreder to make sure our dynamic `components` are not get destroyed we can wrap it in `<keep-alive>`. `keep-alive` now makes sure that our dinamic component is kept alive. 

**App.vue**

```html
<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12">
                <button @click="selectedComponent = 'app-quote'">Quote</button> 
                <button @click="selectedComponent = 'app-author'">Author</button> 
                <button @click="selectedComponent = 'app-new'">New</button> 
                <hr>
                <keep-alive>                <!--use keep alive keyword-->
                <component :is="selectedComponent">  
                <p>Default Content</p>
                </component> 
                </keep-alive>        
            </div>
        </div>
    </div>
</template>

<script>
import Quote from './components/Quote.vue';
import Author from './components/Author.vue';
import New from './components/New.vue';

    export default {
        data: function(){
            return {
                selectedComonent: 'app-quote'    
            }
        },
        components:{
            'app-quote': Quote,     
            'app-author': Author,    
            'app-new': New           
        }
    }
</script>

<style>
</style>
```

Maybe we wanna react to the fact that we navigate away to the other `component` before we could use the `destroyed` lifecycle hook - but now it's no longer called. Do we have another lifecycle hooks? Look in the next class. 