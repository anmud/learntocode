# Single Tour Page

First of all we need to start with a bunch of imports for the `tour-template`. 

**tour-template**

```jsx
import React from 'react'
import {graphql} from 'gatsby'
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import styles from '../css/template.module.css'
import Img from 'gatsby-image'
import {FaMoneyBillWave, FaMap} from 'react-icons/fa'
import AniLink from "gatsby-plugin-transition-link/AniLink"



const Template = ({data}) => {

const {name, price, country, days, description:{description}, images, start, journey} = data.tour

const [mainImage, ...tourImages] = images



    return (
     <div>{data.tour.name}</div>
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
          src
        }
      }
    }
  }
`

export default Template;
```

Now we'll need to create a component by the name of `day`, cos we'll need a section with the day agenda. In components directory let's create `singleTour` folder, and within this folder we'll create a `Day` component. And then import this component to the template.

**Day**

```js
import React from 'react'

const Day = () =>{
  return (
      <div>
          hello
      </div>
  )
}

export default Day;
```

Let's start rendering a single page for each tour.

**tour-template**

```js
import React from 'react'
import {graphql} from 'gatsby'
import Layout from `../components/Layout`
import StyledHero from `../components/StyledHero`
import styles from `../css/template.module.css`
import Img from `gatsby-image`
import {FaMoneyBillWave, FaMap} from `react-icons/fa`
import AniLink from "gatsby-plugin-transition-link/AniLink"
import Day from `../components/SingleTour/Day`


const Template = ({data}) => {

const {name, price, country, days, description:{description}, images, start, journey} = data.tour

const [mainImage, ...tourImages] = images



    return (
   <Layout>
     <StyledHero img={mainImage.fluid}/>
     <section className={styles.template}>
      <div className={styles.center}>
         <div className={styles.images}>
           {tourImages.map((item, index) => {
             return <Img key={index} fluid={item.fluid} alt="single tour" className={styles.image}/>
           })}
         </div>
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

After we got our images let's add some more elements as well as our `day` component with two props: info and day, that we got from our query.

**tour-template**

```js
import React from 'react'
import {graphql} from 'gatsby'
import Layout from '../components/Layout'
import StyledHero from '../components/StyledHero'
import styles from '../css/template.module.css'
import Img from 'gatsby-image'
import {FaMoneyBillWave, FaMap} from 'react-icons/fa'
import AniLink from "gatsby-plugin-transition-link/AniLink"
import Day from '../components/SingleTour/Day'


const Template = ({data}) => {

const {name, price, country, days, description:{description}, images, start, journey} = data.tour

const [mainImage, ...tourImages] = images



    return (
   <Layout>
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
           {cointry}
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
      </div>
         <AniLink fade to="/tours" className='btn-primary'>back to tours</AniLink>
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

