# Gatsby Node

The second step. We'll gonna be working with gatsby-node and the difference in our case will be that we'll gonna be looking for the data from the Contentful. First we need to create a file and the name of the file is important - `gatsby-node.js`, we need to create it in the root project folder.
Within this file we need to export `createPages` function. 
Actually we have two options of the `function` => use it with a `promise` or with `callback`. 

```js
// Promise API
exports.createPages = () => {
  return new Promise((resolve, reject) => {
    // do async work
  })
}

// Callback API
exports.createPages = (_, pluginOptions, cb) => {
  // do Async work
  cb()
}
```

We destructure two things from the `function` - `graphql` and `actions`. Within the actual `function` body we'll destructure one more thing - from the `actions` give me one more function => `createPage`. 

**gatsby-node.js**

```jsx
exports.createPages = async({graphql, actions}) => {
   const {createPage} = actions
}
```

Now we would like to setup `async-await` and setup our `graphql`, basically we would want to run this `function` and within this `function` (await function) we would like to place our query. What we gonna be looking for via the `query`? In our case we gonna be looking for `Contentful`, for all the tours, and within the tours we gonna be looking for the `field` of `slug`.

**gatsby-node.js**

```jsx
exports.createPages = async({graphql, actions}) => {
  const {createPage} = actions

  const {data} = await graphql(`
  query{
    tours: allContentfulTour{
      edges{
        node{
          slug
        }
      }
    }
  }
  `)
}
```

Now we do have `await function` which is set equal to `data` - that would be our main `object` that we are obviously getting, the `edges` inside will represent our `list of tours` and we gonna loop through that list, and for each item in the list we wanna run `createPage` function.  

> Well, we can first see the data we got, but **note** that we need first to restart the server. Actually after every change in the `gatsby-config` file we need to restart the `server`.
> To see the data we gonna look in the `terminal` not in within the actual browser

**gatsby-node.js**

```jsx
exports.createPages = async({graphql, actions}) => {
  const {createPage} = actions

  const {data} = await graphql(`
  query{
    tours: allContentfulTour{
      edges{
        node{
          slug
        }
      }
    }
  }
  `)
  data.tours.edges.forEach(({node}) => {
      createPage({})
  })
}
```

The `createPage` function is looking for an `object`, so we gonna passing an `object` with three `properties`: 
- a path; in our case the path will be `/tours` and then the `slug name`. It's beacuse in our `Tour component` we have the link to navigate to the particular tour, which has a unique `slug` in the link. 

`<AniLink fade className={styles.link} to={`/tours${slug}`}>details</AniLink>`

We can as well omit the `/tours` in the path and leave just the `slug` and that will aslo work, but we'll do this for our site. 

**gatsby-node.js**

```jsx
exports.createPages = async({graphql, actions}) => {
  const {createPage} = actions

  const {data} = await graphql(`
  query{
    tours: allContentfulTour{
      edges{
        node{
          slug
        }
      }
    }
  }
  `)
  data.tours.edges.forEach(({node}) => {
      createPage({
          path:`tours/${node.slug}`
      })
  })
}
```

Next, we are in fact looking for the `component` - that ia actually our `template` - and basically we ganna be setting up the path. Well, and here we need to use  the `node module` by the name of `path`. In order to get this module we'll go to the top of `gatsby-node` file and we just gonna require it - `const path = require("path")`. Then we have a method by the name of `resolve` and now within this `method` we can pass our `path` to the `template`.

**gatsby-node.js**

```jsx
const path = require("path")

exports.createPages = async({graphql, actions}) => {
  const {createPage} = actions

  const {data} = await graphql(`
  query{
    tours: allContentfulTour{
      edges{
        node{
          slug
        }
      }
    }
  }
  `)
  data.tours.edges.forEach(({node}) => {
      createPage({
          path:`tours/${node.slug}`,
          component: path.resolve("./src/templates/tour-template.js"),
      })
  })
}
```

Last one is the `context` - it will be an `object` and within the `context` we'll gonna pass the property name and then we need to setup the value. Why we do this?  Eventually, we'll gonna setup in our `template` the `page query`, this `page query` will gonna use `variables` which we havent's used before and the `value` for that `variable` will be that unique `slug`. So, what's gonna happen is - the moment we click on the specific tour it will gonna fetch the information about this unique `slug`.  

**gatsby-node.js**

```jsx
const path = require("path")

exports.createPages = async({graphql, actions}) => {
  const {createPage} = actions

  const {data} = await graphql(`
  query{
    tours: allContentfulTour{
      edges{
        node{
          slug
        }
      }
    }
  }
  `)
  data.tours.edges.forEach(({node}) => {
      createPage({
          path:`tours/${node.slug}`,
          component: path.resolve("./src/templates/tour-template.js"),
          context:{
              slug: node.slug
          }
      })
  })
}
```

Now we can restart the server. And our specific tour pages were created. 

![tour-template](./tour-template.png)

