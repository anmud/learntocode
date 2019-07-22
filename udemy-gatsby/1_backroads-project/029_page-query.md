# Page Query

We can only run `page queries`in the `components` that are locates in the `page directory`. So, only in our progect pages. 
In order to run the `page query`we go to our `blog.js`page file. If console log the `props` here, we'll see an object with some properties. 

**blog.js**

```jsx
import React from 'react'
import Layout from '../components/Layout'

const Blog = (props) => {

  console.log(props)

  return (
      <Layout>
          <p>My Blog</p>
      </Layout>
  )
}

export default Blog;
```

![blog-props](../blog-props.png)

We are interested in one specific property, which we don't have currently on this object - we need `data` property, and the reason is that we don't run our page query.

In order to setup `page query` we need to import a `tagged template function` (`graphql`) from gatsby, and the syntax will be the following: 
first we need to export it and setup the `variable` and we can call this `variable` how we would like. Then we use `graphql`with the backticks and inside we can write our query. 

**blog.js**

```jsx
import React from 'react'
import Layout from '../components/Layout'
import {graphql} from 'gatsby`

const Blog = (props) => {

  console.log(props)

  return (
      <Layout>
          <p>My Blog</p>
      </Layout>
  )
}

export const query = graphql`
query{
  site{
    siteMetadata{
      title
      description
      author
    }
  }
}
`


export default Blog;
```

What is interesting here - now we have in the `props` the `data`property. Now we just need to come up with the way how we would like to render it. 

**blog.js**

```jsx
import React from 'react'
import Layout from '../components/Layout'
import {graphql} from 'gatsby`

const Blog = ({data}) => {

  return (
      <Layout>
          <p>My Blog</p>
          <h1>title: {data.site.siteMetadata.title}</h1>
      </Layout>
  )
}

export const query = graphql`
query{
  site{
    siteMetadata{
      title
      description
      author
    }
  }
}
`


export default Blog;
```
