# Why we need build tools for front end projects

As a front-end developer you have a ton of different `libraries` and `technologies` that you have to manage all the time. On a professional scale, professional websites require so many assets, and so many different technologies to be used all the time, it gets really hard to manage cos we actually have to decide at what time all of those libraries are going to run. We can't just throw everything onto the page and hope that it all runs at the right time. 

**General principles that all build tools have in common, and how Webpack fits into that role**

`Build tools` will manage all our `assets` so that we don’t have to be combining them all into a single file (or sometimes a few files). We create a `set of rules `for the build tool to follow, telling it specifically how we want each type of asset handled, and then it follows our rules, takes all the assets and bundles them into a single large file, which has everything loading in the correct order and is much easier for us to deal with. Typically, files with names like `bundle` or `main` are the result of a build tool combining many assets into one.

What does it look like to write these `rules` for a `build tool`? `Rules` are written into `config files`. Just to give you a glimpse of where we’re headed, here is an example `webpack config file`. Don’t worry, this should look like gibberish right now, but we’re just going to take a look at a few things.


```js
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.join(__dirname, 'dist'),
    filename: 'main.js',
  },
  module: {
       rules: [
          {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: "babel-loader",
          },
          {
                test: /\.html$/,
                use: [{ loader: "html-loader"}],
                },
                {
                    test: /\.scss$/,
                    use: [ 'style-loader', 'css-loader', 'sass-loader' ]
                }
       ]
 },
  plugins: [
    new HtmlWebPackPlugin({
           template: "./src/html/index.html",
           filename: "./index.html",
    })
  ]
}
```

One thing to notice is that we’re in `javascript` land! You can see that this `config file` is 100% normal javascript. `Webpack` is entirely built with js.

You can also see a whole section here in the middle titled `“rules”`. Not surprisingly, this is where we declare the `rules` that will govern our different `assets`. You might also have noticed that each `rule` targets a certain `type of file with regex`.

> **Build tools** *allow developers to automate their process for handling website assets, saving them lots of time and headache*. 

**some comon names of build tools:**

- Grunt
- Gulp
- Brunch
- Webpack
- Bower
- NPM

---
> **Interview Question**
> Explain what role build tools play in modern frontend development.

---


# Getting Started with Webpack

The webpack documentation describes itself this way:

> *At its core, webpack is a static module bundler for modern JavaScript applications.*

But…what does that really mean?

This image from the Webpack website is a good visual.

![webpack](./webpack.png)

The idea here is that on the left you have all the various `asset file formats` you will probably come across in a project. You might not recognize all the extensions, but just imagine that these are all your `images`, `stylesheets`, `javascripts` and more.

`Webpack` takes all the `assets` on the left and “bundles” or combines them into fewer files that are much easier to manage. Notice that multiple `.js` files on the left became one `.js` file on the right - that’s because the two files were combined into one large `.js file`.

**These tasks would be performed by webpack:**

- running Typescript files
- configure a develoopmant server
- Base64 encoding image files
- adding dynamic css references to html
- run a linter


---
**Interview Question**

Tell us how you have addressed an issue caused by conflicting asset files (or if you haven't experienced this first hand, tell us about a situation where this could happen). Examples could be styles conflicting with a third party stylesheet, or a bug caused by the order of javascript files.

situation: Multiple assets emit different content to the same filename

---

---
**Interview Question**

What information can go into a package.json file? Name everything you can think of.

*Things that must be in your answer*: 

- Npm scripts Dependencies (should mention dev dependencies vs general dependencies) 
- App information (name, version, license, etc..) 

*Potential answers for this question:* 

- Github repo name 
- Starting point 
- NPM privacy

The `package.json` file is kind of a manifest for your project. It can do a lot of things, completely unrelated. It’s a central repository of configuration for tools, for example. It’s also where npm and yarn store the names and versions of the package it installed. 
There are no fixed requirements of what should be in a package.json file, for an application. The only requirement is that it respects the JSON format, otherwise it cannot be read by programs that try to access its properties programmatically.

If you’re building a `Node.js` package that you want to distribute over npm things change radically, and you must have a set of properties that will help other people use it. We’ll see more about this later on.

This is another `package.json`:

```js
{
  "name": "test-project"
}
```

It defines a name property, which tells the name of the app, or package, that’s contained in the same folder where this file lives.

Here’s a much more complex example, which I extracted this from a sample Vue.js application:

```js
{
  "name": "test-project",
  "version": "1.0.0",
  "description": "A Vue.js project",
  "main": "src/main.js",
  "private": true,
  "scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "test": "npm run unit",
    "lint": "eslint --ext .js,.vue src test/unit",
    "build": "node build/build.js"
  },
  "dependencies": {
    "vue": "^2.5.2"
  },
  "devDependencies": {
    "autoprefixer": "^7.1.2",
    "babel-core": "^6.22.1",
    "babel-eslint": "^8.2.1",
    "babel-helper-vue-jsx-merge-props": "^2.0.3",
    "babel-jest": "^21.0.2",
    "babel-loader": "^7.1.1",
    "babel-plugin-dynamic-import-node": "^1.2.0",
    "babel-plugin-syntax-jsx": "^6.18.0",
    "babel-plugin-transform-es2015-modules-commonjs": "^6.26.0",
    "babel-plugin-transform-runtime": "^6.22.0",
    "babel-plugin-transform-vue-jsx": "^3.5.0",
    "babel-preset-env": "^1.3.2",
    "babel-preset-stage-2": "^6.22.0",
    "chalk": "^2.0.1",
    "copy-webpack-plugin": "^4.0.1",
    "css-loader": "^0.28.0",
    "eslint": "^4.15.0",
    "eslint-config-airbnb-base": "^11.3.0",
    "eslint-friendly-formatter": "^3.0.0",
    "eslint-import-resolver-webpack": "^0.8.3",
    "eslint-loader": "^1.7.1",
    "eslint-plugin-import": "^2.7.0",
    "eslint-plugin-vue": "^4.0.0",
    "extract-text-webpack-plugin": "^3.0.0",
    "file-loader": "^1.1.4",
    "friendly-errors-webpack-plugin": "^1.6.1",
    "html-webpack-plugin": "^2.30.1",
    "jest": "^22.0.4",
    "jest-serializer-vue": "^0.3.0",
    "node-notifier": "^5.1.2",
    "optimize-css-assets-webpack-plugin": "^3.2.0",
    "ora": "^1.2.0",
    "portfinder": "^1.0.13",
    "postcss-import": "^11.0.0",
    "postcss-loader": "^2.0.8",
    "postcss-url": "^7.2.1",
    "rimraf": "^2.6.0",
    "semver": "^5.3.0",
    "shelljs": "^0.7.6",
    "uglifyjs-webpack-plugin": "^1.1.1",
    "url-loader": "^0.5.8",
    "vue-jest": "^1.0.2",
    "vue-loader": "^13.3.0",
    "vue-style-loader": "^3.0.1",
    "vue-template-compiler": "^2.5.2",
    "webpack": "^3.6.0",
    "webpack-bundle-analyzer": "^2.9.0",
    "webpack-dev-server": "^2.9.1",
    "webpack-merge": "^4.1.0"
  },
  "engines": {
    "node": ">= 6.0.0",
    "npm": ">= 3.0.0"
  },
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "not ie <= 8"
  ]
}
```

there are lots of things going on here:

- **name** sets the application/package name
- **version** indicates the current version
- **description** is a brief description of the app/package
- **main** set the entry point for the application
- **private** if set to true prevents the app/package to be accidentally published on npm
- **scripts** defines a set of node scripts you can run
- **dependencies** sets a list of npm packages installed as dependencies
- **devDependencies** sets a list of npm packages installed as development dependencies
- **engines** sets which versions of Node this package/app works on
- **browserslist** is used to tell which browsers (and their versions) you want to support

All those properties are used by either npm or other tools that we can use.

[more detailed here](https://flaviocopes.com/package-json/) 
[and here](https://dev.to/easybuoy/understanding-the-package-json-file-3fdg)
[and the docs](https://docs.npmjs.com/files/package.json)

---


# Install Webpack

> Remember that if you ever get stumped or break your code, you can always check out a fresh start from the git repo. You can check out a specific git branch from a repo with this command:
> `git clone --single-branch --branch <branchname> <remote-repo>`

This course is created, the most recent stable version of `Webpack` is version `4`. `Webpack 4` comes with some significant changes from previous versions, so you will find different information out there if you read an older tutorial.

One of the new things about version `4`, is that `webpack` declared a few `default settings` that are automatically in place when you install `webpack`. So, you might not even need a `webpack config file`. Our `app` won’t be following all the default settings, so we will need a custom `config file`, but it’s just a cool thing that `webpack` changed.

So, first things first, we need to `install webpack`. It is an `npm package`, so we run our usual `npm install command`, and while we’re at it, we’ll install the `CLI tool` as well. A `CLI tool` is a pretty common thing you’ll see accompanying developer tools. Its a `terminal program` that allows you to run `commands` from the `command line` and you install it like a normal `npm package`, so we will install both of these at the same time:

`npm i webpack webpack-cli`

> Remember that *npm i* is just shorthand for *npm install*.

You have been successful when you see `webpack` and `webpack-cli` added to your `package.json` dependencies.


One of the things that's unique to `webpack`, and one of the things that it does that othe build tools don't - is that it's going to build a **dependency tree** for us. That `dependency tree` is going to start in one file and then as `Webpack` goes through that file, it's gonna look for other dependancies that that file requires. 

> Webpack has knowledge of the entire stucture of our application. 

In order to build any map like that Webpack gonna need a starting place that we call **entry point**. To setup pur own `entry point` or to setup a `customized configs` that are outside of that `default Webpack settings` that thy've created in `Webpack4 version`, we're gonna use the file called `webpack.config.js`. 


**our project starting files** 

![our-project-starting-files](./our-project-starting-files.png)

2. First in our `client` folder let's create `webpack.config.js` file. 


![our-project-starting-files-2](./our-project-starting-files-2.png)

With this file we'll actually be able to override all those `default values`. 
2. Let's add some necessary `require statements` and `module.exports` to `config` file. 

**webpack.config.js**

```js
const path = require('path')
const webpack = require('webpack')

module.exports = {
    
}
```

3. add a new webpack `npm script` to your `package.json`

`"build":"webpack"`

**package.json**

```js
{
  "name": "example-project",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/server/index.js",
    "build": "webpack", // add here
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": "",
  "dependencies": {
    "express": "^4.17.1",
    "webpack": "^4.41.6",
    "webpack-cli": "^3.3.11"
  }
}
```

4. try running webpack (you should get a Webpack error in terminal, but you'll see it trying to run)

`npm run build`

---
**Interview Question**

At work, a project requires the use of a technology that is completely new to you. What steps would you take to learn the required technology?

1. Identify & articulate a real problem to solve
2. Create a knowledge roadmap
3. Start with basic concepts
3. Find some tutorials on real projects, try them
4. Play with YouTube, copy some projects
5. Get your hands dirty and practice
6. Go deep

> Companies want to understand your process, and they really want to know that you are confident and capable of picking up new languages quickly. Most importantly with questions like this, show that you have a process for learning and let your hard work learning code shine to highlight just how quickly you pick up these topics.

---

# Webpack Entry Point

`The Entry Point` is a first major concept of Webpack, and what it's gonna do is to give us a starting place for Webpack to begin to build its dependancy tree.

So, what we need to do is setup that `entry point` for Webpack in our `webpack.config.js` file. 

Now we need to add an `NPM script` that allows us to run Webpack. To do this we need to go to our `package.json` file and add ` "build": "webpack"` in the scripts. This `script` is just goingg to run the `webpack command`. Nom, we gonna add more to the actual command later. 

**package.json**

```js
{
  "name": "example-project",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/server/index.js",
    "build": "webpack", // add here
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": "",
  "dependencies": {
    "express": "^4.17.1",
    "webpack": "^4.41.6",
    "webpack-cli": "^3.3.11"
  }
}

```

Now, in our `webpack.config.js` file we are going to add `an enrty`. Webpack in Version 4, has a default entry, but in our case we need a custom entry. 

`Webpack` is going to make a map of our `app assets` and all of their `dependencies`, but it needs somewhere to start. *The default location* for the webpack entry point is `./src/index.js` - but because we are already set up with `express` and have a slightly different file structure, that file doesn't exist! Instead, we need to tell `webpack` to use a *custom entry point*. For us, that will be:

`’./src/client/index.js’`

**webpack.config.js**

```js
const path = require('path')
const webpack = require('webpack')

module.exports = {
    entry: './src/client/index.js',  //add enrty here 
}
```

That is gonna be the starting poing where `webpack` will begin to buid our tree from. Now, that we have this `enrty point` declaired, we can go and run webpack in the terminal - `npm run build`. 

When we do that we'll see the error, but in this case the error is a good error. And we are getting this error cos we can't resolve `src`. 

`ERROR in Entry module not found: Error: Can't resolve './src' in '/Users/anastasia/Desktop/coding/fend-webpack-content'`

Really, what this is telling us in a not so great way, is that the `client/index.js` file *doesnt't exist* and we need to create it. 

Let's create a new file called `index.js` inside the `src/client` filder.  

![webpack-enrty-point](./webpack-enrty-point.png)

Once we have that we'll be able to run webpack and successfully see it bult. 

We should see in terminal that `main.js` file was created and that it is `0` bytes. This means that webpack was successful.

If we go to our `index.js` file we wanna something to show up. 

**client/index.js**
```js
alert("I EXIST")

```

Now we should see that reflected in our new built file. When that runs we can now see that `main.js` file was created and that it is `17` bytes. 

If we now go to ouf folder structure, we'll see a new folder - `dist`. It's been generated by webpack. 


![webpack-enrty-point-2](./webpack-enrty-point-2.png)

Inside the `dist` folder we now have `main.js` file, which is exactly what webpack said that it build and if we take a liik through it  - *all the code inside has been generated by webpack.* 


---

**Interview Question**

Without using build tools, what are the strategies available to you for loading assets in a particular order?


answer: have several scripts in index.html ???

---

# Output and Loaders

We have setup webpack just enough to be performing the most basic function of webpack - creating a dist folder with a `main.js` file from our entry point. And all of that is great - but none of it is useful yet.

What’s wrong? Let’s take a look:

1. The distribution folder has no connection whatsoever to our app(view). If you start the `express server`, our app is still functioning exactly the same way it did in part `0`.
2. The `main.js` file of our distribution folder contains none of the javascript or other assets we wrote for our webpage.


In short - there are some things wrong with our distribution folder. So it’s time to take a look at customizing the webpack output. The `“output”` of webpack is - no surprise here - the distribution folder. It is where webpack drops or “outputs” the neat bundles of assets it creates from the individual files we point it to.
So we are going to solve the issues above by setting up our `webpack output`, along with a few other tasks required to make it all work.

> Well, the `src` folder - it's all the folders that **you** create, all of the asset files that **you** write, and all of those files that you are going to edit. 

> The `dist` folder - is for giving out to all of the web pages as thy're run, so  *your website that's running for a client or for a user on the browser*, is going to reference the `dist` folder, not the `src` folder. 

> When you go to edit a file and you wanna that change to be seen on the web page, you can change it in the `build file` (in the dist), you'll see the change immediately, but **it won't be permanent**, and if you wanna have the change permanently, then **you need to change the `src files` and rebuild** in order to have those changes into the `build folder`. 

So, in our `index.html` (the view ) we see that the `assets` that we are bringing in  - are the `styles` and `js` files that we've created and there is a `direct reference` to those files in the source, but that's not what we need anymore. 

```html
 <script>
         <script type="text/javascript" src="/js/nameChecker.js"></script>
        <script type="text/javascript" src="/js/formHandler.js"></script>
        <link rel="stylesheet" href="/styles/resets.css">
        <link rel="stylesheet" href="/styles/base.css">
        <link rel="stylesheet" href="/styles/header.css">
        <link rel="stylesheet" href="/styles/form.css">
        <link rel="stylesheet" href="/styles/footer.css">
```

**index.html**

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <title>Test</title>
        <script>
         <script type="text/javascript" src="/js/nameChecker.js"></script>
        <script type="text/javascript" src="/js/formHandler.js"></script>
        <link rel="stylesheet" href="/styles/resets.css">
        <link rel="stylesheet" href="/styles/base.css">
        <link rel="stylesheet" href="/styles/header.css">
        <link rel="stylesheet" href="/styles/form.css">
        <link rel="stylesheet" href="/styles/footer.css">
    </head>

    <body>

        <header>
            <div class="">
                Logo
            </div>
            <div class="">
                navigation
            </div>
        </header>

        <main>
            <section>
                <form class="" onsubmit="return handleSubmit(event)">
                    <input id="name" type="text" name="input" value="" onblur="onBlur()" placeholder="Name">
                    <input type="submit" name="" value="submit" onclick="return handleSubmit(event)" onsubmit="return handleSubmit(event)">
                </form>
            <section>

            <section>
                <strong>Form Results:</strong>
                <div id="results"></div>
            </section>
        </main>

        <footer>
            <p>This is a footer</p>
        </footer>

    </body>
</html>

```

Now we actually need to `reference` the `dist folder` for all of those. So we are going to add a new `reference` to the `dist main.js` file. 

```html
<script type="text/javascript" src="../../../dist/main.js"></script>
```

And we can just get rid of other scripts. 

**index.html**

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <title>Test</title>
        <script type="text/javascript" src="../../../dist/main.js"></script> <!--have just one line here-->
    </head>

    <body>

        <header>
            <div class="">
                Logo
            </div>
            <div class="">
                navigation
            </div>
        </header>

        <main>
            <section>
                <form class="" onsubmit="return handleSubmit(event)">
                    <input id="name" type="text" name="input" value="" onblur="onBlur()" placeholder="Name">
                    <input type="submit" name="" value="submit" onclick="return handleSubmit(event)" onsubmit="return handleSubmit(event)">
                </form>
            <section>

            <section>
                <strong>Form Results:</strong>
                <div id="results"></div>
            </section>
        </main>

        <footer>
            <p>This is a footer</p>
        </footer>

    </body>
</html>
```
 
 Our `html file` is now referencing the correct `distribution file`, but we still have a problem with this code that we need to address and that issue is that our `index.js` (in client folder) file is not taking in any of the JavaScript that we've already built. So, it fact it has no connection to the files that we have in `client/js folder`. In our `client/js folder` we have two files that we need to bring into the `client/index.js` file. 

To do this a common thing that developers will choose to do is to add a tool called **Babel**. `Babel` is a specialised tool that translates one version of JS to another. And it will allow us to use newer versions of JS and the syntax for them, even though the browser doesn't run those natively. 

In the end it will allow us to do is run `import statements` inside of our `index.js` file, in order to bring in the other JS files that we've written.

So, in the next step we gonna install via npm `Babel` and some of the `presets` that Babel needs in order to work with webpack, just in order to be setup. 

`npm i -D @babel/core @babel/preset -env babel-loader` 

or 

`npm install --dev @babel/core @babel/preset -env babel-loader`

it means that we're installing it to `development`. This means that all of the packages that we're installing right now are not for the `production side` of our application, they don't need to be present when we are actually serving our app to users, instead these are just going to be available during the development process. 

`Babel` requires a configuration file. At the root level of our project let's add a new file `.babelrc`. And add some preset configurations. 

**babelrc** file

```js
{
    'presets': ['@babel/preset-env']
}
```

Now we can use Babel to import all of our JS files, and we have access to ES6 syntax, so we can use `import`. 

**index.js**

```js
import { checkForName } from './js/nameChecker'
import { handleSubmit } from './js/formHandler'

console.log(checkForName);

alert("I EXIST")
console.log("CHANGE!!");
```

So, now we have the reference to our `nameChecker` as well as `formHandler` functions. In the files with our functions we need **export** the function, this what allows us to import the file to the `index.js` 

**nameChecker,js**

```js
function checkForName(inputText) {
    console.log("::: Running checkForName :::", inputText);
    let names = [
        "Picard",
        "Janeway",
        "Kirk",
        "Archer",
        "Georgiou"
    ]

    if(names.includes(inputText)) {
        alert("Welcome, Captain!")
    }
}

export { checkForName } //export function 
```

Babel is the this that allows us to use ES6, it's taking this ES6 syntax and turning it into normal JS for our browsers. 

> But in order to use Babel there is one more thing that we need to do and it takes us into our next webpack concept - `loaders`. 

If we come back to our `webpack.config.file` we gonna all **rules** here - these are **loaders** and JS webpack uses `loaders` and `plug-ins` to achieve the `bundling` of all of our assets. 

Here is an example of the `loader` and in particular `babel loader`. 

```js
module.exports = {
    entry: './src/client/index.js',
    mode: 'development',
    devtool: 'source-map',
    stats: 'verbose',
    module: {
        rules: [
            {
                test: '/\.js$/',
                exclude: /node_modules/,
                loader: "babel-loader"
            }
        ]
    },

}
```

This is the first time when we gonna use `rules` in Webpack. We use `regex` - ` test: '/\.js$/',` - to isolate the type of a file that we are going to run this `loader` on. In this case we are looking for anything that ends in `.js`. 

So, when webpack generates the `dependency tree` it's gonna have the whole bunch of different types of files that are in the `dependency tree`. Our rule is saying that any of those asset files that end in `.js`, need to be treated or run through this particular `loader`.  

So, when we import a file to `client/index.js`, it becomes a dependancy that webpack will search through and find. 

It might seem strange that we have to add ANOTHER library before we’re even finished setting up the first library - but believe me, that’s how it goes. Babel itself is also not an easy tool to use necessarily, it requires a bit of setup but it is widely used throughout the javascript world to translate new ES syntax into vanilla js that can run on browsers etc. They describe their tool like this:

Babel is a toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments.

>I have personally found it helpful to have babel even on projects that don’t have Webpack. Sometimes I’ll install it just for the convenience … like the convenience of no semicolons or being able to use import/export syntax.

---

**Interview Question**

What is the difference between source code and built code?

*Source code*

Source code is a human-readable text written in a specific programming language. For example, the text of a program written in C, C++, C#, Java, etc. is considered source code.

The goal of the source code is to set exact rules and specifications for the computer that can be translated into the machine’s language. 

The source code is often transformed by an assembler or compiler into binary machine code that can be executed by the computer. 

Can be changed over time.

Serves as input to the compiler.	

*Object Code / Build code*

Object Code is the machine executable file having instructions for the machine in the form of binary digits, generated by the compiler.

Last point about Object Code is the way the changes are reflected. When the Source Code is modified, each time the Source Code needs to be compiled to reflect the changes in the Object Code.

Needs to compile the Source Code each time a change is to be made.

It is the output of the compiler after it processes the source code. 

The term build may refer to the process by which source code is converted into a stand-alone form that can be run on a computer or to the form itself. One of the most important steps of a software build is the compilation process, where source code files are converted into executable code. The process of building software is usually managed by a build tool. Builds are created when a certain point in development has been reached or the code has been deemed ready for implementation, either for testing or outright release.

A build is also known as a software build or code build.

---

# Loaders

In the last section we got `webpack’s output` configured - but to use `babel` we had to add a `loader` to our `webpack config`. We used it then without knowing what it was, but now we can revisit it.

Let’s take another look at that `loader`.

```js
module: {
    rules: [
        {
            test: '/\.js$/',
            exclude: /node_modules/,
            loader: "babel-loader"
        }
    ]
}
```

Now take a look at how Webpack describes loaders:

> *Out of the box, webpack only understands JavaScript and JSON files. Loaders allow webpack to process other types of files and convert them into valid modules that can be consumed by your application.*

So `loaders` allow us to *transform files of one type into another type* so that webpack can work with them. It might not have looked like we were transforming file types in the step shown above, but we were actually taking `vanilla js files` and running the `babel-loader` over them to turn them into `es6` files.

There are all sorts of `loaders for webpack` - take a look at this [list](https://webpack.js.org/loaders/). In webpack, most of the things you need to do will end up needing a `loader`.

We will visit a few more loaders later, but for now, just notice how they work. `The rules array` will contain all of our `loaders`, each `loader` *specifies what types of files it will run on by running a `regex matcher`* - in the case above we are looking for all `.js` files - the `$` at the end simply means that nothing comes after that.

But simply looking for all the `.js` files in our project would be problematic, as we don’t want to run this on all the files we have in our `node modules`. For that kind of use case, we also have an `exclude option` available to us, and then we simply name the `loader` to be run on the selected files. *Some loaders will have different options, you can always look it up in the loader documentation*.

[webpack loader documentation](https://webpack.js.org/loaders/)

---
**Interview Question**

What are some examples of es6 syntax? Do you have a favorite?

Arrow functions, template literals, spread syntax and destructuring are my favourite.

---

# Plugins

`Plugins` are one of the last vital concepts for webpack. The Webpack documentation explains them like this:

> While loaders are used to transform certain types of modules, plugins can be leveraged to perform a wider range of tasks like bundle optimization, asset management and injection of environment variables.

So, pretty much anything that we need to do that falls outside the range of `loaders` will be accomplished with `plugins`.

Plugins can do all sorts of things, from automatically adding `asset references` to an `html` file (which we’ll cover in a second) to allowing for `hot module replacement` - which is used in `React’s Create React App` to create an auto updating development server.

`Plugins` are our way to use Webpack to do actions that aren't just turning one type of file to another. 

So, with `loaders` we were *just* taking in JS files, and we're tyrning out Vanilla JS files. We were using `Babel loader` to turn ES6 that we wrote into Vanilla JS.

But whenever we have an action that isn't just turning one file to another, then we need to use a `plugin`. 

The first `plugin`  that we gonna install is called **`HTML Webpack plugin`**. Wnat `HTML Webpack plugin` is gonna do - is allow Webpack to *add a dynamic reference to our dist folder* without us having to do it. 

A lesson ago when we added **a hard-coded reference in the HTML to the JS files**

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <title>Test</title>
        <script type="text/javascript" src="../../../dist/main.js"></script>
    </head>
...
```

we not gonna need that anymore. We're going instead just rely on Webpack to *add the reference at the bottom of our HTML file* `dynamically`. 

When you go to install a `plugin` - the first thing you should actually do is `install it into your node modules`. 

For the `HTML Webpack plugin` we are going to run an ` npm i --save-dev html-webpack-plugin`. 
While that's running, we are also going to go back to our `webpack.config.file`, and we need to do some setup here to actually tell Webpack to use `HTML Webpack plugin`. 

- the first thing is to add a reference to the `HTML Webpack plugin` that is living in our `node modules` folder now. 
- we also need to tell Webpack *when* to run that plugin. In the `plugin section` we are declaring a new instance of the HTML WEbpack plugin, and we are telling it to look at the `html file` in `client/views` and to have it generate the new index HTML file for us in the `dist folder`.

**webpack.config.js**

```js
const path = require('path')
const webpack = require('webpack')
const HtmlWebPackPlugin = require("html-webpack-plugin")  //add a reference
const { CleanWebpackPlugin } = require('clean-webpack-plugin')

module.exports = {
    entry: './src/client/index.js',
    mode: 'development',
    devtool: 'source-map',
    stats: 'verbose',
    module: {
        rules: [
            {
                test: '/\.js$/',
                exclude: /node_modules/,
                loader: "babel-loader"
            },
        ]
    },
    plugins: [
        new HtmlWebPackPlugin({
            template: "./src/client/views/index.html",
            filename: "./index.html",
        }),
    ]
}
```

The cool thing about this is that now when we rerun our command (`npm run build`) now in our `dist folder` we have also `index.html` file 

![webpack-plugins](./webpack-plugins.png)

At the bottom of this file we're getting the `script` that is bringing in the `main.js` file from the distribution folder. 

**dist/index.html**

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <title>Test</title>
        <link rel="stylesheet" href="/styles/resets.css">
        <link rel="stylesheet" href="/styles/base.css">
        <link rel="stylesheet" href="/styles/header.css">
        <link rel="stylesheet" href="/styles/form.css">
        <link rel="stylesheet" href="/styles/footer.css">
    </head>

    <body>

        <header>
            <div class="">
                Logo
            </div>
            <div class="">
                navigation
            </div>
        </header>

        <main>
            <section>
                <form class="" onsubmit="return handleSubmit(event)">
                    <input id="name" type="text" name="input" value="" onblur="onBlur()" placeholder="Name">
                    <input type="submit" name="" value="submit" onclick="return handleSubmit(event)" onsubmit="return handleSubmit(event)">
                </form>
            <section>

            <section>
                <strong>Form Results:</strong>
                <div id="results"></div>
            </section>
        </main>

        <footer>
            <p>This is a footer</p>
        </footer>

    <script type="text/javascript" src="main.js"></script></body> <!--script here-->
</html>
```

What it means is that we can go to our `source index.html` file and remove the `script tag` that is `hard-coded`. 

Why it's important to have this `HTML Webpack plugin` generate the `script` for us instead of us just doing it ourselves? Well, if you ever get into slightly more advanced things like `cache busting`, this strategy of having Webpack generate the `html file` for you allows you to **create dynamic references to certain versions of your asset files** which becomes really handy. 

> One last thing, because we've now decided to use this dynamic reference to the `main.js` file, something else has changed about aour app that's really important to notice. We are no longer referencing the `index.html` file that we are writing (in the source/views/index.html), insted our app is actually gonna rely on the `index.html` file in the `dist folder`. !!!! BUT right now our server doesn't know that at all. 

So, we gonna go to the `server folder` and we're going to take a look at the `index.js` file. 

**source/server/index.js**

```js
var path = require('path')
const express = require('express')
const mockAPIResponse = require('./mockAPI.js')

const app = express()

app.use(express.static('src/client')) //the home root is now in the client

console.log(__dirname)

app.get('/', function (req, res) {
    res.sendFile('/client/views/index.html', { root: __dirname + '/..' }) //reference to source code
})

// designates what port the app will listen to for incoming requests
app.listen(8080, function () {
    console.log('Example app listening on port 8080!')
})

app.get('/test', function (req, res) {
    res.send(mockAPIResponse)
})
```

Right now to generate the home or the root page for our application, we're finding the `client/views/index.html` file. That's what `Express` is looking at to generate the `view` that we find. BUT now we actually don't need a reference to that file, we need a reference to the `dist/index.html` file. 

**source/server/index.js**

```js
var path = require('path')
const express = require('express')
const mockAPIResponse = require('./mockAPI.js')

const app = express()

app.use(express.static('dist')) // we changed the home root to the dist

console.log(__dirname)

app.get('/', function (req, res) {
    res.sendFile('dist/index.html')  //reference to dist
})

// designates what port the app will listen to for incoming requests
app.listen(8080, function () {
    console.log('Example app listening on port 8080!')
})

app.get('/test', function (req, res) {
    res.send(mockAPIResponse)
})
```

Now `Express` knows where to find the correct version of our `index.html` file.

---

**QUESTION 1:**

Would a `webpack plugin` or `loader` be responsible for `creating global constant values` that can be used throughout the application?

answer: a plugin

**QUESTION 2:**

Would a webpack plugin or loader be responsible for taking a `.less` file and returning css?

answer: a loader

**QUESTION 3:**

What are the three steps to install most plugins:?

options: 

- declare a new instance of the plugin in the plugins list
- require the plugin from the node modules directory
- install the plugin via npm or yarn
- instantiate the plugin at the top of the file

answer: 

1. install the plugin via npm or yarn
2. require the plugin from the node modules directory
3. declare a new instance of the plugin in the plugins list

---

---
**Interview Question**

In `javascript`, when you see the `"new"` keyword, what does it do and what does it say about the thing it is being called on?

It does 5 things:

- It creates a new object. The type of this object is simply object.
- It sets this new object's internal, inaccessible, `[[prototype]] (i.e. __proto__)` property to be the constructor function's external, accessible, prototype object (every function object automatically has a prototype property).
- It makes the `this` variable point to the newly created object.
- It executes the constructor function, using the newly created object whenever `this` is mentioned.
- It returns the newly created object, unless the constructor function returns a `non-null` object reference. In this case, that object reference is returned instead.

> Note: constructor function refers to the function after the `new` keyword, as in

`new ConstructorFunction(arg1, arg2)`

[read here](https://stackoverflow.com/questions/1646698/what-is-the-new-keyword-in-javascript)
[and here](https://www.tutorialsteacher.com/javascript/new-keyword-in-javascript)


---

# Mode

The last `core Webpack concept` we’re going to cover is **Mode**. When you build, you probably noticed the warning:

`WARNING in configuration. The 'mode' option has not been set, webpack will fallback to 'production' for this value.`

The issue is that we haven’t told `webpack` which `mode` to run in. **Modes** won’t make sense until we delve into **environments**. You have probably already come across the idea of `environments` in code projects, or at least heard mention of a `“development”` or `“prod”` `environment`. But in order to use webpack to its true potential, we have to fully understand these concepts.

**Production vs. Development Environments**

Developers refer to the various “states” of a website as `environments`. When we are developing a website, we call it the `development environment` - we run the server on `localhost` and use tools that are specifically convenient for us as developers. On the other hand, there is a `production environment`, which is our code on a `server` and where we can tune every tool and file for optimal efficiency, thereby giving our users the best experience when they use the webpage. There can be many environments for a project, like a `testing environment` or `review environment`, but we are going to focus on development and production for now.

There are lots of `tools` that aim to make writing code easier for developers. One of these tools, called `“sass”`, we will cover in a future lesson, but for now just know that it is `css` with some *developer friendly syntax and features*. It’s great that we have tools that make development easier, but if you take `sass` as an example - we can’t run `sass` on a `server`. 

All our `sass files` have to be run through a transpiler in order to become `css` that can go on a live webpage. No matter how awesome a `development tool` is, in the end our code will be judged by how well it runs on a `server`, and *oftentimes what is best for the server is the opposite of what is convenient for developers*. 

So how do we handle both of these `environments`? By utilizing `build tools`, we can make `code` that is convenient for our `dev team`, without sacrificing speed on the `server`.

One of the awesome features of `webpack`, is that it lets us apply configurations to our code based on the `environment` we are running. We can create a `development environment` (**MODE** in webpack) and run totally different `loaders` and `plugins` than we do for `production mode`.

Now we have learned **the second part of why we use build tools**. 
- First, we learned that `build tools` allow devs to use the tools that are more convenient for them. 
- The other side of that coin is that build tools simultaneously allow devs to optimize code for the server. Build tools like Webpack are one tool we can use to help us with organization in all environments. If that doesn’t fully make sense now, don’t worry too much, it will become more clear as we go along.

![webpack-modes](./webpack-modes.png)

In the Webpack there are two ways you can set the `environment mode`: 

- you can either do it through the `CLI tool` and in your terminal
- set that in the `webpack.config` file 

Inside of your `webpack.config` file you can add a `mode` flag by adding a `mode attribute` to the module exports. 

```js
module.exports = {
    entry: './src/client/index.js',
    mode: 'development',
}
```

In your webpack file you could ceate `conditionals` that check for a `production` or `development` mode. BUT that can get a little bit messy and you end up with a lot of logic that't similar but different and right on top of each other. 

So, in order to keep our `webpack.config` cleaner, we'll create two separate `webpack.config` files: one for the `development` (`webpack.dev.js`) mode and the other for the `production` (`webpack.prod.js`) mode. 

Now we need to be able to run these files. BUT currently our `package.json` file has a very generic `build command`, 

`"build": "webpack`

and instead we need the `build command` that's going to reference the `dev` and `prod` files respectively. We need to replace our old command with some `specialized scripts`. 

**package.json**

```js
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/server/index.js",
    "build-prod": "webpack --config webpack.prod.js",
    "build-dev": "webpack-dev-server  --config webpack.dev.js --open"
  },
```

We now have `build-prod` and `build-dev` and they respectively go to `webpack.prod.js` and `webpack.dev.js`.

Now, that these two files are pointing to the correct files, we can run them separately and that's really where Webpack gives us a lot of flexibility, is I can pretend to be in `production mode` and all it takes is me just running a slightly different command - which is awesome.

---

**Interview Question**

Would you minify files for development or production? Why?

Minifying is for production. 

Minification is the process of minimizing code and markup in your web pages and script files. It’s one of the main methods used to reduce load times and bandwidth usage on websites. Minification dramatically improves site speed and accessibility, directly translating into a better user experience.

When creating HTML, CSS and JavaScript (JS) files, developers tend to use spacing, comments and well-named variables to make code and markup readable for themselves. It also helps others who might later work on the assets. While this is a plus in the development phase, it becomes a negative when it comes to serving your pages. Web servers and browsers can parse file content without comments and well-structured code, both of which create additional network traffic without providing any functional benefit.

To minify JS, CSS and HTML files, comments and extra spaces need to be removed, as well as crunch variable names so as to minimize code and reduce file size. The minified file version provides the same functionality while reducing the bandwidth of network requests.

---

# Convenience in Webpack

As you probably noted during this lesson so far, there are some things about the process we have now that aren’t exactly smooth. Overall, I wouldn’t call our set up a good dev experience and we don’t have production set up at all. It is functional, and that’s about it. But the whole point of using all these tools is to make our lives easier. So...what’s going wrong? Let’s use what we’ve learned to make some improvements.

One of the most popular tools for making Webpack convenient to use is called - `webpack-dev-server`.  The `webpack-dev-server` allows you to create a `server for development mode only` and it allows you to run files and run updates immediately. It's what allows `create react app` to have that `hot reloading feature` which is do nice. 

Right out of the box `webpack` provides the ability to watch the certain files. When we say "watch" it means that `Webpack` is going to watch the entire `dependancy tree` to see when you make changes to those files. And you can run this directly by adding `--watch` into the command. 

**package.json**

```js
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/server/index.js",
    "build-prod": "webpack --config webpack.prod.js",
    "build-dev": "webpack  --config webpack.dev.js --watch --info-verbosity verbose" // add watch
  },
```

When we add `--watch` into the file, you can see that when we run the `command` smth different will happan - *Webpack never finishes running*. It's just waiting for the new files or waiting for smth to happen. In fact, it's watching all of our files to see if smth happens.

But it's not quite ergonomic as some people hope for and it can't just restart your browser. The big thing is that if I'm working with this and I have my `localhost` setup - even if I save a file (with new changes) in `client/index.js` and webpack knows to rebuild my `dist folder`, I still have to *refresh my browser* to see the changes that were made. 

So, if we don't wanna refresh the browser to see the changes, webpack has the `webpack-dev-server`, and that will allow  the `hot reloading feature`. 

To install the `webpack-dev-server` we're going to stop the `server` and install 

`npm i -D webpack-dev-server`

Once that's finished loading we can just add the `webpack-dev-server` to our command in our `package.json` file. 

**package.json**

```js
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/server/index.js",
    "build-prod": "webpack --config webpack.prod.js",
    "build-dev": "webpack-dev-server  --config webpack.dev.js --open" // add dev sever
  },
```

This line tells the Webpack that we gonna use the `dev server` to run this `webpack.dev.js` file. And we gonna open it (`--open`) automatically every time when we run it. 

> Up next, have you noticed how we often have to remove the `dist` folder manually before re-running the `build script`? From what I have seen, when you `rebuild`, new code will be added to the `bundled files`, but if there was old code that you got rid of, `webpack build` does not remove the old stuff. So, we have been removing the `dist` folder via the `terminal` and before rebuilding.

Really though, that is an extra and unnecessary step. If we wanted to go really low tech, we could just edit our build script:

`rm -rf dist && webpack-dev-server  --config webpack.dev.js --open`

And there’s really nothing wrong with that. Honestly, being comfortable customizing your npm scripts will make so many things easier. But, it is doing a little bit of extra work. That *script blindly deletes everything* and then rebuilds it, *even if 99% of the code remained the same*.

To be a little more efficient, there is a webpack plugin called **Clean**. From its documentation:

> By default, this plugin will remove all files inside webpack's `output.path` directory, as well as all `unused webpack assets` after every successful rebuild.

Now, some people will choose to go with the simpler blanket dist folder delete, but just to try it, lets install the clean plugin.

`npm i -D clean-webpack-plugin`

Then, as we learned before, to make `webpack` *use* a plugin, we have to do two things:

1.  Add a `require statement` to the top of the `webpack config file`:

`const { CleanWebpackPlugin } = require('clean-webpack-plugin');`

2. Add the `plugin` to Plugins array in the `module.exports`. The `clean plugin` is a good example of a plugin that allows for various options. Take a look at this:

We could use `CleanWebpackPlugin` like this:

`new CleanWebpackPlugin()`

And the above would function. When there are no options passed in, a plugin will run all the default settings, but we can also pass in our custom selections of the various plugin options, like this:

**webpack.dev.js**

```js
new CleanWebpackPlugin({
                // Simulate the removal of files
                dry: true,
                // Write Logs to Console
                verbose: true,
                // Automatically remove all unused webpack assets on rebuild
                cleanStaleWebpackAssets: true,
                protectWebpackAssets: false
        })
```

You can’t know what options a plugin allows without reading the documentation for that plugin.

Add that code to your `wepack.dev.js` file and rerun the `build script`, now you’ll see a few lines added to the webpack output that tell you the `clean plugin` is functioning.

![clean-plugin](./clean-plugin.png)

---

QUESTION:

What do you think are the most time-saving developer tools for you? Which tools do you absolutely want in a development environment, or which could you do without?

answer could be: browser dev tools, git, build tools, linters, debugging tools

**Interview Question**

You start work on a project with webpack already installed, but there is no specific build for production. Walk me through the steps of setting up a production environment in webpack.

answer: 

1. create webpack.config file for the production mode
2.  as well as rename the general config file to the dev mode
3. setup two files respectively (set the mode in the webpack config files)
4. in package.json setup the correct scripts for the modes respectively

[read more here](https://webpack.js.org/guides/production/)

---

**Source Mapping**

We encourage you to have `source maps` enabled in production, as they are useful for `debugging` as well as `running benchmark tests`. That said, you should choose one with a fairly quick build speed that's recommended for production use. For this guide, we'll use the source-map option in the production:

**webpack.prod.js**

```js
 const merge = require('webpack-merge');
  const common = require('./webpack.common.js');

  module.exports = merge(common, {
    mode: 'production',
+   devtool: 'source-map',
  });
```

> Avoid `inline-***` and `eval-***` use in production as they can increase bundle size and reduce the overall performance.

---

**Exercise: Convenience Optional Tasklist**

If you feel comfortable with the things we’ve learned so far, I highly recommend you try out this fun `Bundle Analyzer`. It will give you a graphical representation of all the bundles in your code. We’ve done enough hand holding, so try this one on your own!

- installation instructions are [here](https://www.npmjs.com/package/webpack-bundle-analyzer)
- you've been successful when you can generate the webpage that shows you all of your bundles. 

---

If you want to go further with webpack, check out these topics next:

- [Multiple entry points with webpack](https://github.com/webpack/webpack/tree/master/examples/multiple-entry-points)
- [Cache busting with webpack](https://webpack.js.org/guides/caching/)
- [Using webpack to be more efficient with your styles and assets](https://www.jonathancreamer.com/advanced-webpack-part-1-the-commonschunk-plugin/)