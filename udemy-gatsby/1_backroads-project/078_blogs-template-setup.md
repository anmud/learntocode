# Blogs Template Setup

Let's create one more template - for our blogs with pagination. First we create `blog-list-template` in the templates folder. 

**BlogList**

```js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/Layout"
import styles from "../css/blog.module.css"
import AniLink from "gatsby-plugin-transition-link/AniLink";
import BlogCard from '../components/Blog/BlogCard'
import Title from '../components/Title'


const BlogList = ({ data }) => {
 
  return (
    <Layout>
     
    </Layout>
  )
}


export default BlogList;
```

Next we need to setup our logic in `gatsby-node`. Well, we already get our posts, now we need to setup more logic for additional variables. 

- We'll gonna run `createPage` function. First we wanna know how many posts we wanna get - `const posts = data.posts.edges`. 
- Next we need to come up with how many posts per page we gonna get - `const postsPerPage = 5`. 
- Next we gonna do a little bit of math in order to calculate how many pages we gonna have, depending on how many posts we are getting back, as well as how many posts per page we would want - `const numPages = Math.celi(posts.length/posts/PerPage)`. 
- Next we gonna use `array.from()` method - depending on how many items we have within our array in fact we'll gonna run our `createPages` function. 
- Inside this method we'll run `createPage` function: our properties won't gonna change - we still have the `path` property and we'll need a bit of logic: 'if my current index is zero, my path will be '/blogs', if the current index is one then my path is '/blogs/' - ${i + 1}' - in this case index will be dynamic. Then we would need to use `path resolve`, and as we resolving we need to point to our particular template - `component: path.resolve('./src/templates/blog-list-template.js')`.
- Next we would want to pass the `variables` down - `context: {limit: postsPerPage, }`, we also need `skip` and it will be dynamic - `context: {limit: postsPerPage, skip:  }` - so, for each item in our array we have the index, if the index is `0` that is our first page, we can just multiply that by the amount of posts that we are looking for. Next we pass number of pages as well as the current page. 

**gatsby-node.js**

```js
const path = require("path")

exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions

  const { data } = await graphql(`
    query {
      tours: allContentfulTour {
        edges {
          node {
            slug
          }
        }
      }
      posts: allContentfulPost {
        edges {
          node {
            slug
          }
        }
      }
    }
  `)
  data.tours.edges.forEach(({ node }) => {
    createPage({
      path: `tours/${node.slug}`,
      component: path.resolve("./src/templates/tour-template.js"),
      context: {
        slug: node.slug,
      },
    })
  })
  data.posts.edges.forEach(({ node }) => {
    createPage({
      path: `blog/${node.slug}`,
      component: path.resolve("./src/templates/blog-template.js"),
      context: {
        slug: node.slug,
      },
    })
  })
  const posts = data.posts.edges

  const postsPerPage = 5

  const numPages = Math.celi(posts.length/postsPerPage);

  Array.from({length:numPages}).forEach((_,i)) => {
    createPage({
      path: i === 0 ? `/blogs` : `/blogs/${i + 1 }`,
      component: path.resolve('./src/templates/blog-list-template.js'),
      context: {
        limit: postsPerPage,
        skip: i * postsPerPage,
        numPages,
        currentPage: i + 1,
      }
    })
  };
}
```

We do need to restart the server. 