# Twitter Cards

To test our site and add it e.g to twitter we actually can use [twitter card validator](https://cards-dev.twitter.com/validator).

But first we need to setup the card, we'll do it in our `SEO` component.

**SEO**

```js
import React from 'react'
import {Helmet} from 'react-helmet'
import {useStaticQuery, graphql} from 'gatsby'

const getData = graphql`
query{
    site{
      siteMetadata{
        siteTitle: title
        siteDesc: description
        author
        siteUrl
        image
        twitterUsername
      }
    }
  }
`

const SEO = ({title, description}) => {

const {site} = useStaticQuery(getData)

const {siteDesc, siteTitile, siteUrl, image, twitterUsername} = site.siteMetadata

    return (
      <Helmet htmlAttributes={{lang: 'en'}} title={`${title} | ${siteTitile}`}>
        <meta name='description' content={description || siteDescription}/>
        <meta name='image' content={image}/>

        <meta name='twitter:card' content='summary_large_image'/>
        <meta name='twitter:creator' content={twitterUsername}/>
        <meta name='twitter:title' content={siteTitile}/>
        <meta name='twitter:description' content={description}/>
        <meta name='twitter:image' content={`${siteUrl}${image}`}/>
      </Helmet>
    )
}

export default SEO;
```

