# Facebook Cards

 Next let's do the `facebook card` right before `twitter card`. The idea would be the same, the difference is that `facebook` is looking for `open graph metatags` (`og`). 

**SEO**

```js
import React from "react"
import { Helmet } from "react-helmet"
import { useStaticQuery, graphql } from "gatsby"

const getData = graphql`
  query {
    site {
      siteMetadata {
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

const SEO = ({ title, description }) => {
  const { site } = useStaticQuery(getData)

  const {
    siteDesc,
    siteTitle,
    siteUrl,
    image,
    twitterUsername,
  } = site.siteMetadata

  return (
    <Helmet htmlAttributes={{ lang: "en" }} title={`${title} | ${siteTitle}`}>
      <meta name="description" content={description || siteDesc} />
      <meta name="image" content={image} />
      {/* facebook card */}
      <meta property='og:url' content={siteUrl}/>
      <meta property='og:type' content='website'/>
      <meta property='og:title' content={siteTitle}/>
      <meta property='og:description' content={siteDesc}/>
      <meta property='og:image' content={`${siteUrl}${image}`}/>
      <meta property='og:image:with' content='400'/>
      <meta property='og:height' content='300'/>

      {/* twitter card */}
      <meta name="twitter:card" content="summary_large_image" />
      <meta name="twitter:creator" content={twitterUsername} />
      <meta name="twitter:title" content={siteTitle} />
      <meta name="twitter:description" content={description} />
      <meta name="twitter:image" content={`${siteUrl}${image}`} />
    </Helmet>
  )
}

export default SEO
```

To check the cards we can use [debugger - facebook for developers](https://developers.facebook.com/tools/debug/sharing/batch/), the difference is that you need to be logged in to your facebook account. 





