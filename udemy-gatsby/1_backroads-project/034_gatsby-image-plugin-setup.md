# Image Plugin Setup

`Gatsby image plugin` will help us with the optimisations. And we also need to install two more plugins: `gatsby-transformer-sharp` and `gatsby-plugin-sharp`. 

As the install will be finished we need to restart the server. 

### Brief Overview

Large images will slow down your site, `gatsby-image` helps us with the optimisations cos it provides bunch of things right out of the box; the only thing we need to to is to install the plugin and then setup a specific `qgaphql query`. 

How does `gatsby-image` work?
First we have to import a `componenet` from the `gatsby-image`. Once we imported the `component` there gonna be two `props` : `fixed` prop - for fixed images, and `fluid` prop - for fluid images. Once we setup the `prop` then within the `prop` we'll gonna have to provide the information from our `graphql query`. So, the `value` for the `prop` will be the `value` we are getting from the `query`. 

In our query we are working with `file field` where we have `relativePath` argument, and then we have `childImageSharp` field which we got cos we installed more plugins; within `childImageSharp` we'll have two optional fields: `fixed` or `fluid`, and we have then `...GatsbyImageSharpFixed` - this is a `Fragment`.  A `fragment` is a part of a query that can be used in multiple queries. So, if we pass a `fragment` to the query we pass multiple fields. There is one downside - you won't be able to run the `fragment`  within the `graphiQL` interface. 



```jsx
import React from "react"
import { graphql } from "gatsby"
import Img from "gatsby-image"   //import component

export default ({ data }) => (
  <div>
    <h1>Hello gatsby-image</h1>
     <Img fixed={data.file.childImageSharp.fixed} />    ---  use prop with the needed info ---- 
  </div>
)

export const query = graphql`
  query {
    file(relativePath: { eq: "blog/avatars/kyle-mathews.jpeg" }) {
      childImageSharp {
        # Specify the image processing specifications right in the query.
        # Makes it trivial to update as your page's design changes.
        fixed(width: 125, height: 125) {
          ...GatsbyImageSharpFixed
        }
      }
    }
  }`
```