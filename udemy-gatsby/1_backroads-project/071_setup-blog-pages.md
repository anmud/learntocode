# Setup Blog Pages

Now we would like to setup pages for every blogpost. First we'll setup a template for the blog. And then we need to setup our query (post query) and use this query in the `node.js` file. 

**gatsby-node.js**

```js
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
    posts: allContentfulPost{
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
  data.tours.edges.forEach(({node}) => {
    createPage({
        path:`blog/${node.slug}`,
        component: path.resolve("./src/templates/blog-template.js"),
        context:{
            slug: node.slug
        }
    })
})
}
```

After we finished this step we need to restart the server. 