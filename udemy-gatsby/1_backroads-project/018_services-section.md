# Services Section

The `Services` section we'll create in the `constants` folder, where we'll have icons, title and some information. 

**src/constants/services.js**

```jsx 
import React from "react"
import { FaWallet, FaTree, FaSocks } from "react-icons/fa"

export default [
  {
    icon: <FaWallet />,
    title: "saving money",
    text:
      "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Obcaecati, earum. ",
  },
  {
    icon: <FaTree />,
    title: "endless hiking",
    text:
      "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Obcaecati, earum. ",
  },
  {
    icon: <FaSocks />,
    title: "amazing comfort",
    text:
      "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Obcaecati, earum. ",
  },
]
```
So, once we hae our `constants` tha we'll use in our `Services` section, in our `home` directory let's create a new file `Services.js` 

**home/Services.js**

```jsx
import React from 'react'

const Services = () => {
   return (
       <div>
           
       </div>
   )
}

export default Services;
```

Now we can import it in our `index.js` where we wanna render the `Services` section. 

**index.js**

```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import SimpleHero from '../components/SimpleHero'
import Banner from '../components/Banner'
import About from '../components/Home/About'
import Services from '../components/Home/Services'



export default () => {
   return (
    
       <Layout>
     
      <SimpleHero>
        <Banner  
        title="Some Title"  
        info="Lorem ipsum dolor sit amet, consectetur adipiscing elit,  
        sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.">
          <Link to="/tours" className="btn-white">explore tours</Link>
        </Banner>
      </SimpleHero>

      <About/>
      <Services/>
     
       </Layout>
    
   ) 
} 
```

Now let's continue working with `Services` section styling. First we import our `Title` and styles, as well as we need to import `constants` from `services.js`.  

**home/Services.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/services.module.css'
import services from '../../constants/services'



const Services = () => {
   return (
       <div>
           
       </div>
   )
}

export default Services;
```
Then setup the return and styling. 

**home/Services.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/services.module.css'
import services from '../../constants/services'



const Services = () => {
   return (
       <section className={styles.services}>
           <Title title="our" subtitle="services"/>
           <div className={styles.center}>
               {services.map((item, index) => (
                   <article key={index} className={styles.service}>
                       <span>{item.icon}</span>
                       <h4>{item.title}</h4>
                       <p>{item.text}</p>
                   </article>
               ))}
           </div>
       </section>
   )
}

export default Services;
```
