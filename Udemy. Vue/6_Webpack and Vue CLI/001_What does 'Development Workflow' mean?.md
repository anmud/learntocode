# What does 'Development Workflow' mean?

In more complex applications we might probably have multiple `script imports` and we might have multiple `packages` we use. We wanna bundle them together, we wanna bulld them. So, we have our `code` and when we ship it to a `production server` when the user is able to see it, we wanna transform it for doing so, we wanna apply some special features, that `development workflow` can offer us. 

![development-workflow])(../development-workflow.png)

Special features:
* we can compile single `file templates` in a VueJS application. `Single file` templates is a powerful alternative to using the `el` property and inferring a `template` from the `DOM`, or the `template property`. Basically, the `template` outsurced in the separate file and the `workflow` will be using a special tool in it, which understands this `single file` templates and then is able to compile them 
* use case-insensitive component selectors 
* preprocessors and more

![special-features])(../special-features.png)

Side effect: Compiler removed from the VueJS Package => 30% reduced Package size. 

