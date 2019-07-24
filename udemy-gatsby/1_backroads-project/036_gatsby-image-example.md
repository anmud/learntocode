# Gatsby-Image Example

First let's setup a new `component` (Images.js) in the `examples folder`. We would like to render this `component` on the `Blog` page. So, we need to import `Images` component to the `Blog page`. 

**Images.js**

```jsx
import React from 'react'

const Images = () => {
   return (
      <div>
        hello from images
    </div>
   )
}

export default Images;
```

**Blog.js**

```jsx
import React from 'react'
import Layout from '../components/Layout'
import Images from '../examples/Images'

const Blog = () => {


  return (
      <Layout>
          <p>My Blog</p>
          <Images/>
      </Layout>
  )
}




export default Blog;
```

Now within the `Images.js` component we need to do a bunch of imports: `graphql`, `useStaticQuery` hook, styled components, and one image, and as we wanna use `gatsby-image` plugin we'll import `gatsby Image` component.

**Images.js**

```jsx
import React from 'react'
import {graphql, useStaticQuery} from 'gatsby'
import styled from 'styled-components'
import img from '../images/connectBcg.jpeg'
import Img from 'gatsby-image'


const Images = () => {
   return  (
   <div>
        hello from images
    </div>
   ) 
}

export default Images;
```

So, we would like to create three boxes with the images inside: basic image, fixed image with blur effect, and the fluid image with svg. 
First for this we'll use `styled components` and create a `wrapper` - this will be a simple `div`, within this `div` we'll setup our `css`.

Within the `wrapper` we gonna have three columns, and we'll use the `article`. Inside the first `article` we'll place the basic image using simple import. And let's add some basic styling. 


**Images.js**

```jsx
import React from 'react'
import {graphql, useStaticQuery} from 'gatsby'
import styled from 'styled-components'
import img from '../images/connectBcg.jpeg'
import Img from 'gatsby-image'


const Images = () => {
   return (
     <Wrapper>
         <article>
            <h3>basic image</h3>
            <img src={img} className="basic" alt="basic"/>
         </article>
        
        <article> 
            <h3>fixed image/blur</h3>
        </article>
        
        <article>
            <h3>fluid image/svg</h3>
        </article>
    </Wrapper>
   ) 
}

const Wrapper = styled.div`
  text-align: center;
  text-transform: capitalize;
  width: 80vw;
  margin: 0 auto 10rem auto;

  article{
      border: 3px solid red;
      padding: 1rem 0;
  }

  .basic{
      width: 100%;
  }
`

export default Images;
```

To get our images using `gatsby-image` let's setup our `query`. First we setup a `variable` 

**Images.js**

```jsx
import React from 'react'
import {graphql, useStaticQuery} from 'gatsby'
import styled from 'styled-components'
import img from '../images/connectBcg.jpeg'
import Img from 'gatsby-image'


const getImages = graphql`
 query Images {
    fixed: file(relativePath: {eq: "defaultBcg.jpeg"}) {
      childImageSharp {
        fixed(width: 300, height: 400) {
          src
        }
      }
    }
    fluid: file(relativePath: {eq: "blogBcg.jpeg"}) {
      childImageSharp {
        fluid {
          src
        }
      }
    }
  }
`

const Images = () => {
 return (
    <Wrapper>
        <article>
            <h3>basic image</h3>
            <img src={img} className="basic" alt="basic"/>
         </article>
        
        <article> 
            <h3>fixed image/blur</h3>
        </article>
        
        <article>
            <h3>fluid image/svg</h3>
        </article>
    </Wrapper>
 )  
}

const Wrapper = styled.div`
  text-align: center;
  text-transform: capitalize;
  width: 80vw;
  margin: 0 auto 10rem auto;

  article{
      border: 3px solid red;
      padding: 1rem 0;
  }

  .basic{
      width: 100%;
  }
`

export default Images;
```

Now let's use `useStaticQuery` hook, first we setup a `variable`, let's calll this `data`, and call `useStaticQuery` with `getImages` guery. Well, even though we have the Image `component` , we also need  a `fragment`, we'll use the basic one `GatsbyImageSharpFixed`. So, first in our `second` article we'll use `Image gatsby component` with the `fixed prop` and look for the `data` we are getting back. 

**Images.js**

```jsx
import React from 'react'
import {graphql, useStaticQuery} from 'gatsby'
import styled from 'styled-components'
import img from '../images/connectBcg.jpeg'
import Img from 'gatsby-image'


const getImages = graphql`
 query Images {
    fixed: file(relativePath: {eq: "defaultBcg.jpeg"}) {
      childImageSharp {
        fixed(width: 300, height: 400) {
          ...GatsbyImageSharpFixed
        }
      }
    }
    fluid: file(relativePath: {eq: "blogBcg.jpeg"}) {
      childImageSharp {
        fluid {
          src
        }
      }
    }
  }
`

const Images = () => {

    const data = useStaticQuery(getImages)

 return (
    <Wrapper>
        <article>
            <h3>basic image</h3>
            <img src={img} className="basic" alt="basic"/>
         </article>
        
        <article> 
            <h3>fixed image/blur</h3>
            <Img fixed={data.fixed.childImageSharp.fixed}/>
        </article>
        
        <article>
            <h3>fluid image/svg</h3>
        </article>
    </Wrapper>
 )  
}

const Wrapper = styled.div`
  text-align: center;
  text-transform: capitalize;
  width: 80vw;
  margin: 0 auto 10rem auto;

  article{
      border: 3px solid red;
      padding: 1rem 0;
  }

  .basic{
      width: 100%;
  }
`

export default Images;
```

> Note. If we are using the `fixed prop` make sure we are using `fragment` for `fixed images`. 

Let's add more `css` (@media) and that would be a simple `grid`, basically what we are saying that starting with 992px we gonna have a `grid layout`.

```js
const Wrapper = styled.div`
  text-align: center;
  text-transform: capitalize;
  width: 80vw;
  margin: 0 auto 10rem auto;

  article{
      border: 3px solid red;
      padding: 1rem 0;
  }

  .basic{
      width: 100%;
  }
  @media (min-width: 992px){
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      grid-column-gap: 1rem;
  }
`
```

Concerning the `arguments` (width, height) we are using with the `fixed field` in the `childImageSharp` actually, there are already default ones; if we get rid of our `width` and `height` we still get our image - the problem with that `image`, of course, it will be massive, cos by default the `width` is 400px. So, it's better when we include `width` and `height` in the arguments. 

If we wanna our `image` be black-and-white we can add the argument named "grayscale" - `fixed(grayscale: true)`. 

Now let's work with the `fluid` image. For the fluid image we'll use in the query the `fragment` called `GatsbyImageSharpFluid_tracedSVG`. Now let's setup the `Image component` in the third `article`.

**Images.js**

```jsx
import React from 'react'
import {graphql, useStaticQuery} from 'gatsby'
import styled from 'styled-components'
import img from '../images/connectBcg.jpeg'
import Img from 'gatsby-image'


const getImages = graphql`
 query Images {
    fixed: file(relativePath: {eq: "defaultBcg.jpeg"}) {
      childImageSharp {
        fixed(width: 300, height: 400) {
          ...GatsbyImageSharpFixed
        }
      }
    }
    fluid: file(relativePath: {eq: "blogBcg.jpeg"}) {
      childImageSharp {
        fluid {
          ...GatsbyImageSharpFluid_tracedSVG
        }
      }
    }
  }
`

const Images = () => {

    const data = useStaticQuery(getImages)

 return (
    <Wrapper>
        <article>
            <h3>basic image</h3>
            <img src={img} className="basic" alt="basic"/>
         </article>
        
        <article> 
            <h3>fixed image/blur</h3>
            <Img fixed={data.fixed.childImageSharp.fixed}/>
        </article>
        
        <article>
            <h3>fluid image/svg</h3>
            <Img fluid={data.fluid.childImageSharp.fluid}/>
        </article>
    </Wrapper>
 )  
}

const Wrapper = styled.div`
  text-align: center;
  text-transform: capitalize;
  width: 80vw;
  margin: 0 auto 10rem auto;

  article{
      border: 3px solid red;
      padding: 1rem 0;
  }

  .basic{
      width: 100%;
  }
  @media (min-width: 992px){
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      grid-column-gap: 1rem;
  }
`

export default Images;
```

