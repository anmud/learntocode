# Validating `props`

So, we built our component which uses `props` to get `data` from the parent. Maybe it's a reusable `component` we wanna use in multiple places and in each place it gets different `data`, but of course the type of `data` should always be equal. 
In our example we reversed the `name`, and this will non work if we will pass in a number, or a bolean, it has to be a `string` this component gets. 

**UserDetail.vue file**

```html
<template>
    <div class="component">
        <h3>You may view the User Details here</h3>
        <p>Many Details</p>
        <p>User Name: {{switchName()}}</p>   
    </div>
</template>

<script>
export default{
    props: ['name'],
    methods: {
     switchName(){                                      
      return this.name.split('').reverse().join('');
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
