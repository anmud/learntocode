# How VueJS manages your Data and Methods

We can access the `vue instance` outside as we know. And for example if we can call a `method` - `vm1.show()`. This is proxying. Because in theory , we don't create a `vue instance`, yes we call it. we are creating it with a constructor, but this is an `object` shift with the VueJS framework, the core `object` of that framework. And we don't know which `properties` this has, we can't find out from the API reference, but it clearly doesn't have the properties we set up in the `object` we pass to the constructor - that'is just the argument we give to that constructor. 

Behind the scenes when creating an `instance`, VueJS will take our `object` we pass in, and then it will take our `data` properties and our `methods` and kind of use them as native `properties` on the `vue instance` object itself. It setsup a kind of a watcher of each of these `properties`, which makes sure that it recognises whenever one of these `properties` is changed so that it knows when to update the DOM or when to do anything. 

We are able to access our `properties` form outside, BUT we are not able to create a new `property`.  