# About Image Fix

So, let's get our images using the `query`. In our `About component` which we render in our home page currently we just import the `image`. Now let's get it with the `query`. Let's setup the `query` for the `fluid image`. Surely, instead of `src` we'll use the `fragment` then. 

```jsx

query aboutImage {
  aboutImage:file(relativePath: {eq:"defaultBcg.jpeg"}){
    childImageSharp{
      fluid(maxWidth: 600){
        src
      }
    }
  }
}

```

Them in our `About` component we need to import `useStaticQuery` hook and `graphql`. And now we can setup our `query`. 

**About.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/about.module.css'
import img from '../../images/defaultBcg.jpeg'
import {graphql, useStaticQuery} from 'gatsby'

const getAbout = graphql`
query aboutImage {
  aboutImage: file(relativePath: {eq: "defaultBcg.jpeg"}) {
    childImageSharp {
      fluid(maxWidth: 600) {
        src
      }
    }
  }
}
`

const About = () => {
    return (
      <section className={styles.about}>
       <Title title="about" subtitle="us"/>
       <div className={styles.aboutCenter}>
         <article className={styles.aboutImg}>
           <div className={styles.imgContainer}>
             <img src={img} alt="about company"/>
           </div>
         </article>
         <article className={styles.aboutInfo}>
           <h4>explore the difference</h4>

             <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
              Donec suscipit feugiat odio, sed consequat ligula. Ut cursus, quam eu tristique bibendum, enim eros accumsan nisl, eget posuere dui ante eu tellus. 
               Maecenas tincidunt lacus eget placerat cursus.  
             Nam et volutpat est. Duis convallis risus in efficitur scelerisque.
              </p>

             <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
              Donec suscipit feugiat odio, sed consequat ligula. Ut cursus, quam eu tristique bibendum, enim eros accumsan nisl, eget posuere dui ante eu tellus. 
               Maecenas tincidunt lacus eget placerat cursus.  
             Nam et volutpat est. Duis convallis risus in efficitur scelerisque.
              </p>
             
             <button type="button" className="btn-primary">read more</button>
          
         </article>
       </div>
      </section>
    )
}

export default About;
```

Once we have done this we can use `useStaticQuery` hook, and we'll destructure the `data` we get from the `query`. And we surely also need to import gatsby `Image` component. We'll use  then `fluid` prop for our `Image` component and use the data we need from the `query`. 

**About.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/about.module.css'
//import img from '../../images/defaultBcg.jpeg'
import {graphql, useStaticQuery} from 'gatsby'
import Img from 'gatsby-image'

const getAbout = graphql`
query aboutImage {
  aboutImage: file(relativePath: {eq: "defaultBcg.jpeg"}) {
    childImageSharp {
      fluid(maxWidth: 600) {
        src
      }
    }
  }
}
`

const About = () => {

  const {aboutImage} = useStaticQuery(getAbout)

    return (
      <section className={styles.about}>
       <Title title="about" subtitle="us"/>
       <div className={styles.aboutCenter}>
         <article className={styles.aboutImg}>
           <div className={styles.imgContainer}>
             {/* <img src={img} alt="about company"/> */}
             <Img fluid={aboutImage.childImageSharp.fluid} alt="awesome landscape"/>
           </div>
         </article>
         <article className={styles.aboutInfo}>
           <h4>explore the difference</h4>

             <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
              Donec suscipit feugiat odio, sed consequat ligula. Ut cursus, quam eu tristique bibendum, enim eros accumsan nisl, eget posuere dui ante eu tellus. 
               Maecenas tincidunt lacus eget placerat cursus.  
             Nam et volutpat est. Duis convallis risus in efficitur scelerisque.
              </p>

             <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
              Donec suscipit feugiat odio, sed consequat ligula. Ut cursus, quam eu tristique bibendum, enim eros accumsan nisl, eget posuere dui ante eu tellus. 
               Maecenas tincidunt lacus eget placerat cursus.  
             Nam et volutpat est. Duis convallis risus in efficitur scelerisque.
              </p>
             
             <button type="button" className="btn-primary">read more</button>
          
         </article>
       </div>
      </section>
    )
}

export default About;
```

Now, we need to add `fragment` to our `query` otherwise it won't work. 

**About.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/about.module.css'
//import img from '../../images/defaultBcg.jpeg'
import {graphql, useStaticQuery} from 'gatsby'
import Img from 'gatsby-image'

const getAbout = graphql`
query aboutImage {
  aboutImage: file(relativePath: {eq: "defaultBcg.jpeg"}) {
    childImageSharp {
      fluid(maxWidth: 600) {
        ...GatsbyImageSharpFluid_tracedSVG
      }
    }
  }
}
`

const About = () => {

  const {aboutImage} = useStaticQuery(getAbout)

    return (
      <section className={styles.about}>
       <Title title="about" subtitle="us"/>
       <div className={styles.aboutCenter}>
         <article className={styles.aboutImg}>
           <div className={styles.imgContainer}>
             {/* <img src={img} alt="about company"/> */}
             <Img fluid={aboutImage.childImageSharp.fluid} alt="awesome landscape"/>
           </div>
         </article>
         <article className={styles.aboutInfo}>
           <h4>explore the difference</h4>

             <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
              Donec suscipit feugiat odio, sed consequat ligula. Ut cursus, quam eu tristique bibendum, enim eros accumsan nisl, eget posuere dui ante eu tellus. 
               Maecenas tincidunt lacus eget placerat cursus.  
             Nam et volutpat est. Duis convallis risus in efficitur scelerisque.
              </p>

             <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
              Donec suscipit feugiat odio, sed consequat ligula. Ut cursus, quam eu tristique bibendum, enim eros accumsan nisl, eget posuere dui ante eu tellus. 
               Maecenas tincidunt lacus eget placerat cursus.  
             Nam et volutpat est. Duis convallis risus in efficitur scelerisque.
              </p>
             
             <button type="button" className="btn-primary">read more</button>
          
         </article>
       </div>
      </section>
    )
}

export default About;
```