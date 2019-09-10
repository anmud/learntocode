# Render Images in Rich Text Field

As we know we need as well `images`. What should give us a clue - in our `json` response we should look for the `url`. The we would need to look for the `node type`.

In order to render the images we need to pass `options` object as an argument to our `function` -  `{documentToReactComponents(json, options)}`. And then we need to setup this `object`. This object will gonna have a very special property - `renderNode`, this property will be an `object`; within that `object` we set which `nodeType` we gonna be dealing with, and we need to set this equal to the function; as an argument to the function we pass `node` (node where the `image` is sitting). Our return from the `function` will represent how that `node` is being displayed. 

```js
const options = {
    renderNode: {
      "embedded-asset-block": node => {
        return (
          <div className="rich">
            <h3>this is awesome image</h3>
            <img width="400" src={node.data.target.fields.file["en-US"].url} />
            <p>images provided by john doe</p>
          </div>
        )
      },
    },
  }
```

> Note here the image won't be the `gatsby-image` cos we are not having our fluid property. 

**blog-template**

```js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/Layout"
import styles from "../css/single-blog.module.css"
import AniLink from "gatsby-plugin-transition-link/AniLink";
import { documentToReactComponents } from "@contentful/rich-text-react-renderer"

const Blog = ({ data }) => {
  const {
    title,
    published,
    text: { json },
  } = data.post


const options = {
    renderNode: {
      "embedded-asset-block": node => {
        return (
          <div className="rich">
            <h3>this is awesome image</h3>
            <img width="400" src={node.data.target.fields.file["en-US"].url} />
            <p>images provided by john doe</p>
          </div>
        )
      },
    },
  }
  return (
    <Layout>
      <section className={styles.blog}>
        <div className={styles.center}>
          <h1>{title}</h1>
          <h4>published at : {published}</h4>
          <article className={styles.post}>
            {documentToReactComponents(json, options)}
          </article>
          <AniLink fade to="/blog" className="btn-primary">
            all posts
          </AniLink>
        </div>
      </section>
    </Layout>
  )
}

export const query = graphql`
  query getPost($slug: String!) {
    post: contentfulPost(slug: { eq: $slug }) {
      title
      published(formatString: "MMMM Do, YYYY")
      text {
        json
      }
    }
  }
`

export default Blog;
```


