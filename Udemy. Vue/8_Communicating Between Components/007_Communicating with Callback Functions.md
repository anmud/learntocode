# Communicating with Callback Functions

There is an alternative to working with custom `event` - using a `callback function`. Well, in our parent `component` we can add a method. In our `component tag` in the `User` file we can add another `prop` (in our case `'resetFn'`), which is a pointer to the `resatName` function. 

**User.vue file**

```html
<template>
    <div class="component">
        <h1>The User Component</h1>
        <p>I'm an awesome User!</p>
        <button @click="changeName">Change my Name</button>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-6">
                <app-user-detail :name='name' @nameWasReset="name=$event" :resetFn="resetName"></app-user-detail>           <!--new prop here-->
            </div>
            <div class="col-xs-12 col-sm-6">
                <app-user-edit></app-user-edit>
            </div>
        </div>
    </div>
</template>

<script>
    import UserDetail from './UserDetail.vue';
    import UserEdit from './UserEdit.vue';

    export default {
        data: function (){
            return {
             name: 'Ana'
            }
        },
        methods: {
            changeName(){
                this.name = 'Dimi';
            },
            resetName(){              //new method here 
                this.name = "Ana"
            }
        },
        components: {
            appUserDetail: UserDetail,
            appUserEdit: UserEdit
        }
    }
</script>

<style scoped>
    div {
        background-color: lightblue;
    }
</style>
```

Now in our `UserDetail` file we set a new `prop`. And add a new `button` which executes the `resetFn`. 

**UderDetail file**

```html
<template>
    <div class="component">
        <h3>You may view the User Details here</h3>
        <p>Many Details</p>
        <p>User Name: {{switchName()}}</p>
        <button @click="resetName">Reset the Name</button>
        <button @click="resetFn()">Reset the Name</button>    <!--new button-->
    </div>
</template>

<script>
export default {
    props: {
        name: {
            type: String
            },
        resetFn: Function   //add new prop here
            },
    methods: {
     switchName(){
      return this.name.split('').reverse().join('');
     },
     resetName(){
         this.name = "Max";
         this.$emit('nameWasReset', this.name)
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
Well, this is just another setup to avoid working with a `custom event`. 