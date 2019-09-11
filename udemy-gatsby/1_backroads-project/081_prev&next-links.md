# Prev and Next Links

First let's make the structure, the first link will be before the first number and the next will be after.

```js
  <section className={styles.links}>
     <AniLink fade to="/blogs" className={styles.link}>Previous</AniLink>

          {Array.from({length: numPages}, (_,i) => {
            return <AniLink fade key={i} to={`/blogs/${i === 0 ? "" : i+1}`}  className={i + 1 === currentPage? `${styles.link}${styles.active}` : `${styles.link}`}>{i+1}</AniLink>
          })}


          <AniLink fade to="/blogs" className={styles.link}>Next</AniLink>
     </section>
```

Now we need to do a little bit of calculation => we gonna be checking what is current page, and we remember that the current page is changing, since that value is changing what we can do here is - we can setup some kind of variable - `const nextPage = /blogs/${currentPage + 1}`. Now we can change the `to` prop in the link to the `nextPage` variable. 

```js
  <section className={styles.links}>
     <AniLink fade to={nextPage} className={styles.link}>Previous</AniLink>

          {Array.from({length: numPages}, (_,i) => {
            return <AniLink fade key={i} to={`/blogs/${i === 0 ? "" : i+1}`}  className={i + 1 === currentPage? `${styles.link}${styles.active}` : `${styles.link}`}>{i+1}</AniLink>
          })}


          <AniLink fade to={nextPage} className={styles.link}>Next</AniLink>
     </section>
```

Next let's setup the logic for the previous page. We'll have a variable which will be equal to the ternary operator: if the current page minus one is equal to one then i would navigate to `/blogs`, if not - to `/blogs/${currentPage - 1}`  - `const prevPage = currentPage - 1 === 1 ? `/blogs`: `/blogs/${currentPage - 1}`.

**blog-list-template**

```js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/Layout"
import AniLink from "gatsby-plugin-transition-link/AniLink"
import styles from "../css/blog.module.css"
import BlogCard from "../components/Blog/BlogCard"
import Title from "../components/Title"

const BlogList = props => {
  
  const { currentPage, numPages } = props.pageContext
  const { data } = props
  const nextPage = `/blogs/${currentPage + 1}`
  const prevPage = currentPage - 1 === 1 ? `/blogs`: `/blogs/${currentPage - 1}` 



  return (
    <Layout>
      <section className={styles.blog}>
        <Title title="latest" subtitle="posts" />
        <div className={styles.center}>
          {data.posts.edges.map(({ node }) => {
            return <BlogCard key={node.id} blog={node} />
          })}
        </div>
        <section className={styles.links}>
        <AniLink fade to={prevPage} className={styles.link}>Prev</AniLink>

          {Array.from({ length: numPages }, (_, i) => {
            return (
              <AniLink
                key={i}
                fade
                to={`/blogs/${i === 0 ? "" : i + 1}`}
                className={
                  i + 1 === currentPage
                    ? `${styles.link} ${styles.active}`
                    : `${styles.link}`
                }
              >
                {i + 1}
              </AniLink>
            )
          })}

          <AniLink fade to={nextPage} className={styles.link}>Next</AniLink>

        </section>
      </section>
    </Layout>
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

Though there are two more things that we are going to setup so we don't navigate to the `pages` that don't exist. First there gonna be a `variable` that gonna be checking whether the `current page` is equal to 1, whether we are sitting in the first page. And the `last page` - if the current page is equal to number of pages. 

```js

  const isFirst = currentPage === 1;
  const isLast = currentPage === numPages
```

Now we can use the `and operator` within jsx and only show the previous button if we are sitting on page number one, and conditionally render the next button only if we are not sitting on the last page. 

```jsx
{
            !isFirst &&  <AniLink fade to={prevPage} className={styles.link}>Prev</AniLink>
}
```

```jsx
{
          !isLast && <AniLink fade to={nextPage} className={styles.link}>Next</AniLink>
}
```

**blog-list-template**

```js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/Layout"
import AniLink from "gatsby-plugin-transition-link/AniLink"
import styles from "../css/blog.module.css"
import BlogCard from "../components/Blog/BlogCard"
import Title from "../components/Title"

const BlogList = props => {
  
  const { currentPage, numPages } = props.pageContext
  const { data } = props
  const nextPage = `/blogs/${currentPage + 1}`
  const prevPage = currentPage - 1 === 1 ? `/blogs`: `/blogs/${currentPage - 1}` 

  const isFirst = currentPage === 1;
  const isLast = currentPage === numPages


  return (
    <Layout>
      <section className={styles.blog}>
        <Title title="latest" subtitle="posts" />
        <div className={styles.center}>
          {data.posts.edges.map(({ node }) => {
            return <BlogCard key={node.id} blog={node} />
          })}
        </div>
        <section className={styles.links}>
          {
            !isFirst &&  <AniLink fade to={prevPage} className={styles.link}>Prev</AniLink>
          }
        

          {Array.from({ length: numPages }, (_, i) => {
            return (
              <AniLink
                key={i}
                fade
                to={`/blogs/${i === 0 ? "" : i + 1}`}
                className={
                  i + 1 === currentPage
                    ? `${styles.link} ${styles.active}`
                    : `${styles.link}`
                }
              >
                {i + 1}
              </AniLink>
            )
          })}
        {
          !isLast && <AniLink fade to={nextPage} className={styles.link}>Next</AniLink>
        }
          

        </section>
      </section>
    </Layout>
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

