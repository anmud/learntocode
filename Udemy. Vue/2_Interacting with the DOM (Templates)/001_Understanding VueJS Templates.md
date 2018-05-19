# Understanding VueJS Templates

### **There is one more important thing to understand**

We start with the connection between a `vue instance` and `html` code. By creating new `VueJs instance` and note! that we don't store it in a `variable` - it is still created though. By instantiating this `instance` we do create this connection, and VueJS then takes `html` code, and creates a template based on that code. `VueJS` creates a template based on our `html` code, stores that internally, and then basically uses this template to create a real `html` code which then is rendered as the DOM.  