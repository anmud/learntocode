# Protecting Routes with Guards

There is one thing we will need from time to time. We wanna control if the user is allowed to enter a certain `route` or if he is allowed to leave it. Let's say we load the `UserDetail` page and then we click on `Edit` - we want to control whether the user is allowed to visit the `edit` page, and then if the user was on the `Edit` page we want to control if he is allowed to leave. 

On our `UserEdit` page let's add a button, and only after this `button` is clicked we want the user to navigate away, otherwise if changes weren't confirmed for example we want at least ask the user if he wants to naviagte away. So, we have two check: before the user enters and when he leaves. 

**UserEdit**

```html
<template>
<div>
    <h3>Edit the User</h3>
    <p>Locale: {{ $route.query.locale}}</p>
    <p>Analytics: {{ $route.query.q}}</p>
    <hr>
    <button class="btn btn-primary">Confirmed</button>  <!--add a button--> 
    <div style="height: 700px"></div>  
    <p id="data">Some extra Data</p>
</div>
</template>
```
