# BlogList Component

First within the components folder let's create `blog` folder, within this folder we'll create two files: `BlogList.js` and `Blog.Card` that will be responsible for rendering every post. 

**BlogList**

```js
import React from 'react'
import BlogCard from '../Blog/BlogCard'


const BlogList = () => {
    return (
        <div>
            hello from blog list
             <BlogCard/>
        </div>
    )
}

export default BlogList;
```

**BlogCard**

```js
import React from 'react'


const BlogCard = () => {
    return (
        <div>
            hello from blog card
        </div>
    )
}

export default BlogCard;
```

Now we also need to import our `BlogList` to `blog.js` page. 

blog.js
```js
import React from 'react'
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import {graphql} from 'gatsby'
import BlogList from '../components/Blog/BlogList'

const Blog = ({data}) => {

  const image = data.blogBcg.childImageSharp.fluid

  return (
      <Layout>
        <StyledHero image={image}>
        </StyledHero>
        <BlogList/>
      </Layout>
  )
}




export default Blog;

export const query = graphql`
query{
  blogBcg: file(relativePath: {eq:"blogBcg.jpeg"}){
    childImageSharp{
      fluid(quality:90, maxWidth:4160){
        ...GatsbyImageSharpFluid_withWebp
      }
    }
  }
}
`
```

Let's continue working on `BlogList`. 

BlogList
```js
import React from 'react'
import BlogCard from '../Blog/BlogCard'
import Title from '../Title'
import {useStaticQuery, graphql} from 'gatsby'
import styles from '../../css/blog.module.css'


const getPosts = graphql`
query{
    posts: allContentfulPost( sort: {fields: published, order: DESC }){
      edges{
        node{
          published(formatString: "MMM Do, YYYY")
          title
          slug
          id: contentful_id
          image{
            fluid{
              ...GatsbyContentfulFluid
            }
          }
        }
      }
    }
  }
`

const BlogList = () => {

const {posts} = useStaticQuery(getPosts)

    return (
       <section className={styles.blog}>
        <Title title='our' subtitle='blogs'/>
        <div className={styles.center}>
          {posts.edges.map(({node}) => {
              return <BlogCard key={node.id} blog={node}/>
          })}
        </div>
       </section>
    )
}

export default BlogList;
```



