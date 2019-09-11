# Blog List Template

So, we need to setup our `blog-list-template` and pull the information that we get with the variables in `gatsby-node`. First we need to setup our query. 

**blog-list-template**

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

export const query = graphql`
query getPosts($skip:Int, limit:$Int){
  posts: allContentfulPost(skip:$skip, limit:$limit, sort: {fields: published, order: DESC}){
    edges{
      node{
        slug
        title
        id: contentful_id
        published(formatString: "MMMM Do, YYYY")
        image{
          fluid{
            src
          }
        }
      }
    }
  }
}
`

export default BlogList;
```

Every time we are working with our pages we get the `data` as the `props` and destructure it. In this case we gonna be passing in `props` - in this case we'll destructure `data` which is coming from the `props` - `const {data} = props`.

Once we have access to the `data` we wanna render the list. 

**blog-list-template**

```js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/Layout"
import styles from "../css/blog.module.css"
import AniLink from "gatsby-plugin-transition-link/AniLink";
import BlogCard from '../components/Blog/BlogCard'
import Title from '../components/Title'


const BlogList = (props ) => {
 
const {data} = props

  return (
    <section className={styles.blog}>
     <Title title="latest" subtitle="posts"/>
     <div className={styles.center}>
         {data.posts.edges.map(({node}) => {
           return <BlogCard key={node.id} blog={node}/>
         })}
     </div>
    </section>
  )
}

export const query = graphql`
query getPosts($skip: Int!, $limit: Int!) {
  posts: allContentfulPost(
    skip: $skip
    limit: $limit
    sort: { fields: published, order: DESC }
  ) {
    edges {
      node {
        slug
        title
        id: contentful_id
        published(formatString: "MMMM Do, YYYY")
        image {
          fluid {
            ...GatsbyContentfulFluid
          }
        }
      }
    }
  }
}
`

export default BlogList;
```

