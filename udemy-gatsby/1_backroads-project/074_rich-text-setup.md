# Rich Text Setup

For the help we can go to (`Contentful guides`)[https://www.contentful.com/developers/docs/tutorials/general/rich-text-and-gatsby/] - 'Using Rich Text with Gatsby'.

First we need to install `rich-text-react-renderer`. The way it works - we'll gonna have to look for the `function` by the name of 'documentToReactComponents' => then within that function we'll gonna have to pass our json (as document).

**blog-template**

```js
import React from 'react'
import {graphql} from 'gatsby'
import Layout from '../components/Layout'
import styles from '../css/single-blog.module.css'
import AniLink from "gatsby-plugin-transition-link/AniLink"
import { documentToReactComponents } from '@contentful/rich-text-react-renderer';

const Blog = ({data}) => {

const {title, published, text: {json}} = data.post

    return (
   <Layout>
    <section className={styles.blog}>
      <div className={styles.center}>
        <h1>{title}</h1>
        <h4>published at: {published}</h4>
         <article className={styles.post}>
             {documentToReactComponents(json)}
         </article>
        <AniLink fade to='/blog' className="btn-primary">all posts</AniLink>
      </div>
    </section>
   </Layout>
    )
}

export const query = graphql`
query getPost($slug: String){
    post: contentfulPost(slug: {eq: $slug}){
      title
      published(formatString:"MMMM Do, YYYY")
      text{
        json
      }
    }
  }
`

export default Blog;
```



