# Title Component

In our `components` folder let's create one more folder ("Home"). We'll do this cos there will be some `components` that we will be using globally - all through out the project. However, there are `sections` and/or `components` that will be specific only for the `home page` or only for the `tours page` let's say. 
It will be useful if we'll create a separate folder where all the `components` that let's say we gonna be using for the `home page` will be stored. 

So, in the `components/home` let's create "About.js" file. And setup the `title component` which will be use globally. We'll create the `title component` in the components folder, but we wanna render it in the `About section`. 

The idea is simple - if we know that we wanna use the `styled title component` in all the `sections` we would like to setup some kind of placeholder for that `section`. 

**components/title**

```jsx
import React from 'react'

const Title = () => {
   return (
       <div>
           
       </div>
   )
}

export default Title;
```

And import our `title component` to our `about section` 

**components/home/about**

```jsx
import React from 'react'
import Title from '../Home/About'


const About = () => {
    return (
      <div>
      <Title/>
      </div>
    )
}

export default About;
```

And then, at the very least we would need to import it in one of  the `pages` also. So, in our `index.js` (which is our home page of the site), we'll import the `About section`. 

**index.js**

```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import SimpleHero from '../components/SimpleHero'
import Banner from '../components/Banner'
import About from '../components/Home/About'



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
     
       </Layout>
    
   ) 
} 
```
