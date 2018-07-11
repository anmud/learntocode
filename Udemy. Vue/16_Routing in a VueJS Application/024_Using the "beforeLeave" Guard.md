# Using the "beforeLeave" Guard

Now we wanna check if the user is allowed to leave our `route`. In our `UserEdit` component let's add `script` and export the `object` and there we wanna have `data object`. In the `data` we'll return an `object` where we set `confiirmed` property to `false`. Now we'll add a `click listner` to the button in the template and bind it to `confirmed` property. This controls now whether we click this button or not. And now on the `component` `vue-instance` we can setup `beforeRouteLeave()` method. This is the only place where we can do this, cos this is in the `component` where we wanna check this. And in the `method` we could check if `confirmed` is `true`. From Inside this `method` we have access to the property in the `data object` because we are in the `component`. If this `confirmed` we want to navigate, so we call `next()`, if it is not confirmed we want to show the confirm dialog to let the user decide if he wants to continue, if the user answers "yes" it also navigates, if not we want to stop the navigation (set to false). 

**UserEdit**

```html
<template>
<div>
    <h3>Edit the User</h3>
    <p>Locale: {{ $route.query.locale}}</p>
    <p>Analytics: {{ $route.query.q}}</p>
    <button class="btn btn-primary" @click="confirmed = true">Confirm</button>  <!--add click listner-->
    <div style="height: 700px"></div>  
    <p id="data">Some extra Data</p>
</div>
</template>

<script>
export default{
data(){
    return {
        confirmed: false      //create confirmed property
    }
},
beforeRouteLeave(to, from, next){           //add before leave method
    if (this.confirmed){
     next();
    } else {
     if (confirm ("Are you sure?")) {
         next();
     } else {
       next(false);
     }
    }
}
}
</script>
```