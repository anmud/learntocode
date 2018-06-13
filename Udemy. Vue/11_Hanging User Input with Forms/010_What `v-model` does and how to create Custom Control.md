# What `v-model` does and how to create Custom Control

Let's say we wanna build our own `input`. Let'e build a little `switch`, which we can toggle between `on` and `off`. To do this we will build our own component, which has this logic in it. To build our own component with the `inout` we have to understand what `v-model` does behind the scenes. 
`v-model` does two thing behind the scenes:
* it binds to the `value` of the data property in the object, in our case `userData.email`.   
* it also gives us `@input` listner, which then listens to changes, or `@change` if we use the `lazy` modifyer. In case we have `@input` listner it listens to changes `<@input="userData.email=$event.target.value">` - it sets `userData.email` equal to `$event` that is the normal JavaScript event, there we wanna get access to its element, which was the root for this event - `target` (the input field) - and then `value`. So, this way we can create our `manula v-model`. It's the same thing `v-model` does behind the scenes, but now just in the longer form. 

let's look at our example with 'mail' input:

```html
<div class="form-group">
 <label for="email">Mail</label>
 <input
 type="text"
id="email"
 class="form-control"
 :value="userData.email"      
 @input="userData.email=$event.target.value">    <!--binds to the value, listens to changes-->  
</div>
<div class="form-group">
<label for="password">Password</label>
<input
 type="password"
id="password"
 class="form-control"
 v-model.lazy="userData.password">     
</div>

<script>
    export default {
        data: function(){
            return {
              userData:{         
                email: ' ',
                password: '', 
                age: 27
        },
              message: 'A new text',
              sendMail: [],
              gender: 'Male',
              priorities: ['High', 'Medium', 'Low'],
              selectedPriority: 'High' 
        }
        }
    }
</script>
```

Well, let's create our own component, and name it 'switch'. 