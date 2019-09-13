# Adding SEO to all pages

Next we wanna go to all our pages, including the templates and pass the information that we would want within our SEO. 

**404**

```js
import React from 'react'
import Layout from '../components/Layout'
import styles from '../css/error.module.css'
import {Link} from 'gatsby'
import Banner from '../components/Banner'
import AniLink from "gatsby-plugin-transition-link/AniLink";
import SEO from '../components/SEO'

const Error = () => {
  return (
      <Layout>
        <SEO title='Error'/>
         <header className={styles.error}>
          <Banner title="oops it's a dead end">
            <AniLink fade to="/" className="btn-white">
              back to home page
            </AniLink>
          </Banner>
         </header>
      </Layout>
  )
}

export default Error;
```

**blog**

```js
import React from 'react'
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import {graphql} from 'gatsby'
import BlogList from '../components/Blog/BlogList'
import SEO from '../components/SEO'

const Blog = ({data}) => {

  const image = data.blogBcg.childImageSharp.fluid

  return (
      <Layout>
        <SEO title='Blog'/>
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

**contact**

```js
import React from 'react'
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import {graphql} from 'gatsby'
import ContactComponent from '../components/Contact/Contact'
import SEO from '../components/SEO'

const Contact = ({data}) => {

  const image = data.connectBcg.childImageSharp.fluid

  return (
      <Layout>
        <SEO title='Contact'/>
        <StyledHero image={image}>
        </StyledHero>
        <ContactComponent/>
      </Layout>
  )
}

export default Contact;

export const query = graphql`
query{
  connectBcg: file(relativePath: {eq:"connectBcg.jpeg"}){
    childImageSharp{
      fluid(quality:90, maxWidth:4160){
        ...GatsbyImageSharpFluid_withWebp
      }
    }
  }
}
`
```

And for all other `pages` we'll have the same import. This will be a bit different with the `templates`, cos we wanna `title` for each `blog`. We'll gonna be using dynamic values - the title that we get from our query. 

**blog-template**

```js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/Layout"
import styles from "../css/single-blog.module.css"
import AniLink from "gatsby-plugin-transition-link/AniLink"
import { documentToReactComponents } from "@contentful/rich-text-react-renderer"
import SEO from '../components/SEO'

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
      "embedded-entry-block": node => {
        const { title, image, text } = node.data.target.fields
        console.log(text)

        return (
          <div>
            <br />
            <br />
            <br />
            <br />
            <h1>this is other post : {title["en-US"]}</h1>
            <img
              width="400"
              src={image["en-US"].fields.file["en-US"].url}
              alt=""
            />
            {documentToReactComponents(text["en-US"])}
            <br />
            <br />
            <br />
            <br />
          </div>
        )
      },
    },
  }
  return (
    <Layout>
      <SEO title={title}/>
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

export default Blog
```

**tour-template**

```js
import React from 'react'
import {graphql} from 'gatsby'
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import styles from '../css/template.module.css'
import Img from 'gatsby-image'
import {FaMoneyBillWave, FaMap} from 'react-icons/fa'
import Day from '../components/SingleTour/Day'
import AniLink from "gatsby-plugin-transition-link/AniLink"
import SEO from '../components/SEO'

const Template = ({data}) => {

const {name, price, country, days, description:{description}, images, start, journey} = data.tour

const [mainImage, ...tourImages] = images



    return (
   <Layout>
     <SEO title={name}/>
     <StyledHero img={mainImage.fluid}/>
     <section className={styles.template}>
      <div className={styles.center}>
         <div className={styles.images}>
           {tourImages.map((item, index) => {
             return <Img key={index} fluid={item.fluid} alt="single tour" className={styles.image}/>
           })}
         </div>
         <h2>{name}</h2>
         <div className={styles.info}>
         <p>
           <FaMoneyBillWave className={styles.icon}/>
           starting from ${price}
         </p>
         <p>
           <FaMap className={styles.icon}/>
           {country}
         </p>
         </div>
         <h4>starts on: {start}</h4>
         <h4>duration: {days}</h4>
         <p className={styles.desc}>{description}</p>
         <h2>daily schedule</h2>
         <div className={styles.journey}>
           {journey.map((item, index) => {
             return <Day key={index} day={item.day} info={item.info}/>
           })}
         </div>
         <AniLink fade to="/tours" className='btn-primary'>back to tours</AniLink>
      </div>
     </section>
   </Layout>
    )
}

export const query = graphql`
query($slug:String){
  tour:  contentfulTour(slug:{eq: $slug}){
      name
      price
      country
      days
      start(formatString: "dddd MMMM Do, YYYY")
      description{
        description
      }
      journey{
        day
        info
      }
      images{
        fluid{
          ...GatsbyContentfulFluid
        }
      }
    }
  }
`

export default Template;
```

