# Contact Page

We gonna be setting up our `data` on `external cms` - `"contentful"` - we'll gonna be holding our `tours` as well as the `blog posts` and then we have to access it using the `qraphql`, as well as we gonna rendering the single pages for that particular tour or the blog post. Before we do all of these steps, let's first setup the `Contact` page. 

In the `Contact` page we ganna have the `form`. BUT we have just **static pages**, how can we then get the users information? One of the solution could be the service called - "form spree". When we setup this service we'll be able to get this information. 

First let's create one more folder in the `components` - "Contact". Let's say we wanna have some kind of components for the `Contact` page. In our case it will be only one component. 

**src/components/Contact/Contact.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/contact.module.css'



const Contact = () => {
   return (
      <div>
          hello from contact
      </div>
   )
}

export default Contact;
```

And we gonna render it at `contact.js` page. 

**src/pages/contact.js**

```jsx
import React from 'react'
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import {graphql} from 'gatsby'
import ContactComponent from '../components/Contact/Contact'

const Contact = ({data}) => {

  const image = data.connectBcg.childImageSharp.fluid

  return (
      <Layout>
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

Well, our `Contact` component will have a `section` with the classes from `css.module`. Within the `section` we gonna first start by rendering the `Title` component,after the `title` we gonna start dealing with the centering `div` and within the `div` we gonna have the `form`: in the `form` we gonna have some `divs` and in these `divs` we gonna have some `inputs`.

**src/components/Contact/Contact.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/contact.module.css'



const Contact = () => {
   return (
      <section classNme={styles.contact}>
          <Title title="contact" subtitle="us"/>
          <div className={styles.center}>
            <form className={styles.form}>
              <div>
                  <input type="text" name="name" id="name" className={styles.formControl} placeholder="ana mo"/>
              </div>
              <div>
                  <input type="email" name="email" id="email" className={styles.formControl} placeholder="email@email.com"/>
              </div>
              <div>
                 <textarea name="message" id="message" rows="10" className={styles.formControl} placeholder="hello there"/>
              </div>
              <div>
                  <input type="submit" value="submit here" className={styles.submit}/>
              </div>
            </form>
          </div>
      </section>
   )
}

export default Contact;
```

