# Broken Project

As we have gone along setting up this project, we have let all functionality slide. We just got our styles to show up again, but now, what about our click events? What if we wanted to make an API call or add pages to this app?

Well, our app is broken:

- JS `event code` isn't running
- our `Express server` isn't doing anything
It't important that we *reset* our `Express server` beacause our `production build`, that we also haven't setup yet, is going to rely on our `Express server`. 
- out `production build` isn't setup

1. Let's dive into why our `JS code` isn't working. `Webpack` try to keep the global scope really clean! And we know that it's a good thing to keep the global scope clean. BUT what that means is that Webpack puts all of our code into encapsulated little libraries and that can be a great thing, and it is a great thing. BUT it can also mean tha we have some problems and those problems are actually what are breaking our code right now. 

If you look under the hood of what Webpack is actually doing, Webpack usese **IIFE's** to separate all of our code and keep it neatly organized into its own little chunks. That if what IIFE's are for. 

[read more about IIFE's](https://medium.com/javascript-in-plain-english/https-medium-com-javascript-in-plain-english-stop-feeling-iffy-about-using-an-iife-7b0292aba174)
[and read more about IIFE's](https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6)
[and here](https://stackabuse.com/javascripts-immediately-invoked-function-expressions/)
[and one more time here](https://tylermcginnis.com/javascript-modules-iifes-commonjs-esmodules/)

These little chunks of code *can't always talk to each other* - and that is what is breaking our `event code`.  

Let's take a look at a bit more `JS scope setup`. Webpack is dealing a lot with JS so it encapsulates each chunk of JS into a `scope layer`. You can imagine that if all of our JS code, especially if this were a large application, we could have thouthands of lines of JS, and if `Webpack` didn't encapsulate everythingwe would end up with just all of our stuff thrown into one huge `global scope` and we we would have to make sure that `variable names` didn't conflict with other `variable  names` and it would be chaos like we see in the pickture below ('without scope' part). 

![js-scope](./js-scope.png)

But with `scope` (the left side of the picture) we have these neatly stacked layers and the `IIFE's` are what allow `Webpack` to do that. Now, one problem with that is that sometimes we lose communication between `"function"` and `"global"` scope layers. The `browser events` like our "form submit" are happening on the `global level` but our code - the custom JS that we wrote - is happening  on the `function level`. And our problem is that we lack the communication between these two layers. 

So, what we need to do is come up with a fix that allows our `functions` to to be *callable* by the `global scope` or when a `browser event` happens. 

[MDN docks about IIFE's](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

**Some benefits of using IIFE's:**

- they keep variables out of the global scope
- they run directly after being defined, so you don't have to name them
- when you use them, you don't have to worry about variables you write overlapping with variables from third party code

---

QUESTION: 

What is wrong with this IIFE?

```js
function foo() {
...javascript
}();
```

answer: 

Potentially there are other answers, but the big one that you shouldn’t miss, is that this is an invalid IIFE because it is a named function. If I were asked this in an interview, I wouldn’t stop at saying why it is an invalid IIFE - a question like this is an opportunity to tell the interviewer everything you know about the topic. It isn’t going to far to talk about a time that you used them, or a lightbulb moment you had while learning about it.

---

# Fixing our Functionality 

If we take a look at this code, we added a new section called `"output"`. 

```js
module.exports = {
    entry: './src/client/index.js',
    mode: 'development',
    devtool: 'source-map',
    stats: 'verbose',
    output: {
        libraryTarget: 'var',
        library: 'Client'
    }
}
```

Up untill now, we've use the default settings for `output`. But to make JS work we've added the `library` and `libraryTarget` settings. You just know that our JS files, our custom JS (on the client side), is now going to be put into our own `librarly` that we've called `"Client"`. The name "client" isn't important, you can choose any name. BUT what's important to understand here is that *all of our JS code is now going to be accessable through the `client library`*. 

What does that really mean? How is Webpack going to let us use this new `client library` and how does that help us? 

First of we need to come to our `client/index.js` file that has both of our JS files being imported. 

**client/index.js**

```js
import { checkForName } from './js/nameChecker'
import { handleSubmit } from './js/formHandler'

console.log(checkForName);

alert("I EXIST")
console.log("CHANGE!!");
```

And we are going to actually *export* these files into the `client library`. 

**client/index.js**

```js
import { checkForName } from './js/nameChecker'
import { handleSubmit } from './js/formHandler'

console.log(checkForName);

alert("I EXIST")
console.log("CHANGE!!");

export {               //export to client library
    checkForName,
    handleSubmit
}
```

How it's get to the `client library` it's done by `Webpack` and we don't have to worry about it. Here we just need to know that all of our JS is being exported from the `client/index.js` file and now it's going to be a part of that `client library`. 

But how does that actually get used in our `index.html` ??? If we come to the `client/index.html` and look at the `custom handle submit function` that we've created, this is not goint to work. 

**client/index.html**

```html
 <section>
                <form class="" onsubmit="return handleSubmit(event)">
                    <input id="name" type="text" name="input" value="" onblur="onBlur()" placeholder="Name">
                    <input type="submit" name="" value="submit" onclick="return handleSubmit(event)" onsubmit="return handleSubmit(event)">
                </form>
<section>
```

Now, we can add `client.handleSubmit` and this is going to refernse our `custom function` that is now being exported to the `client library`. 

**client/index.html**

```html
 <section>
                <form class="" onsubmit="return Client.handleSubmit(event)">
                    <input id="name" type="text" name="input" value="" onblur="onBlur()" placeholder="Name">
                    <input type="submit" name="" value="submit" onclick="return Client.handleSubmit(event)" onsubmit="return Client.handleSubmit(event)">
                </form>
<section>
```

And if we make this change universally through this file and through all of our JS, we will have fixed all of our JS issues. 

If we go to our **formHandler.js** file, just know that all throughout any of the JS that you've written *it now need to referense the Client library*. In our example we need to make sure that we referense our `checkForName` function through the `client library`. 

```js
function handleSubmit(event) {
    event.preventDefault()

    // check what text was put into the form field
    let formText = document.getElementById('name').value
    
    Client.checkForName(formText)   //add client here 

    console.log("::: Form Submitted :::")
    fetch('http://localhost:8080/test')
    .then(res => res.json())
    .then(function(res) {
        document.getElementById('results').innerHTML = res.message
    })
}

export { handleSubmit }
```

2. Now let's address what's going wrong with our `Express server`.

We have been using the `webpack-dev-server` in development, which is an awesome tool because we don't have to restart our `browser` every time that we make a style change. We get to watch that update happen in live time in our browser. 
BUT when we use this in production, we can't use the `webpack-dev-server`. So, we need to make sure that our `Express server` is setup correctly so that we can use it in `production`. 

Actually we have been using `webpack-dev-server` that *doesn't rebuld* our `main.js`. So the `main.js` file in the `dist folder` that we are looking at is the same that we've built right before we added the `webpack-dev-server`. 