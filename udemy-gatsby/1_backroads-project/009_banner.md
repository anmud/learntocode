# Banner

Well, we have the `image` now, but we also wanna render something within the `image` => and that's in fact one more `component` (but, surely, we could setup all the logic inside the `SimpleHero` as well). Anyway in case we have a separate `component` for this purpose we then can reuse this many ways as we want. 

So, we'll create a new `component` and call it `Banner`; and a css faile for the `Banner` component. In the `Banner` we'll have the `<h1>` - it will be displaying the `title` prop that we'll pass; also we need to pass `info` and `children` as props -  `children` is an extra option for us in case we wanna render somehting within the `Banner`. Let's say we wanna use `button` in the `SimpleHero` within the `Banner`, so `children` will render the `button` in the `Banner` which itself is rendered by the `SimpleHero` component. 

**Banner**
```jsx
import React from 'react'
import styles from '../css/banner.module.css'

const Banner = ({title, info, children}) => {
    return (
       <div className={styles.banner}>
          <h1>{title}</h1>
         <p>{info}</p>

         {children}
       </div>
    )
}

export default Banner;
```
Now in the `index.js` we need to figure out how it will be rendered. In the `index.js` we need to import the `Banner` component. Since we added the `children` prop, now whatever we ganna render within the `SimpleHero` will be rendered in te center, cos that's te way we setup our css. And we need to pass props for the `Banner` (title, info). 

**index.js**
```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import SimpleHero from '../components/SimpleHero'
import Banner from '../components/Banner'


export default () => {
   return (
    
       <Layout>
     
      <SimpleHero>
        <Banner title="Some Tile"  
        info="Lorem ipsum dolor sit amet, consectetur adipiscing elit,  
        sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."/>
      </SimpleHero>
   
       </Layout>
    
   ) 
} 
```
Well, we also have the `children` props in the `Banner`, and we wanna render a `button` (link to the "tours" page of our site) in the `Banner`. And in order the `link` to be styled we need to add `clasName` - and this is one of the glabal `classNames` we are reusing through out the project. 

**index.js**
```jsx
import React from "react"
import {Link} from "gatsby"
import Layout from '../components/Layout'
import SimpleHero from '../components/SimpleHero'
import Banner from '../components/Banner'


export default () => {
   return (
    
       <Layout>
     
      <SimpleHero>
        <Banner  
        title="Some Tile"  
        info="Lorem ipsum dolor sit amet, consectetur adipiscing elit,  
        sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.">
          <Link to="/tours" className="btn-white">explore tours</Link>
        </Banner>
      </SimpleHero>
   
       </Layout>
    
   ) 
} 
```