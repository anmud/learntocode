# Query SiteMetadata

Next we would like to pull information from  our `siteMetadata` via query and then displaying within our SEO. Our first step is to setup our query. 

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

    return (
      <Helmet htmlAttributes={{lang: 'en'}} title={title}>
        <meta name='description' content={description}/>
      </Helmet>
    )
}

export default SEO;
```

Next we would like to destructure the information we get even more. 

```js
const {site} = useStaticQuery(getData)

const {siteDesc, siteTitile, siteUrl, image, twitterUsername} = site.siteMetadata
```

Now let's change a bit the props for the `helmet`. 

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
        <meta name='description' content={description}/>
      </Helmet>
    )
}

export default SEO;
```

Next, in our case working with `description` we won't do the check of props. BUT for the real project we should do this, the detailed info we can find in `gatsby docs`. In our case we just use the `or` (||) operator. 

```js
<Helmet htmlAttributes={{lang: 'en'}} title={`${title} | ${siteTitile}`}>
        <meta name='description' content={description || siteDescription}/>
</Helmet>
```

And let's add one `more` metatag for the image. 

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
      </Helmet>
    )
}

export default SEO;
```

Now we can use our `seo` component on every page we want ans just pass the props. 