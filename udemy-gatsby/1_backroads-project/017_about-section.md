# About Section

Within the `About us` section we'll use the basic way of importing react images. We need to import our `css module` for the `About` section. First we change the simple `<div>` to the `<section>` and add `className` for the section. 

**About.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/about.module.css'
import img from '../../images/defaultBcg.jpeg'


const About = () => {
    return (
      <section className={styles.about}>
       <Title title="about" subtitle="us"/>
      </section>
    )
}

export default About;
```

Then under the `Title` we add one more `<div>`, inside it we'll place two articles - first will be the `image container`. Within the first `article` we gonna place `image`.

**About.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/about.module.css'
import img from '../../images/defaultBcg.jpeg'


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
       </div>
      </section>
    )
}

export default About;
```

![about-image](./about-image.png)

Then we'll add one more `article`. 

**About.js**

```jsx
import React from 'react'
import Title from '../Title'
import styles from '../../css/about.module.css'
import img from '../../images/defaultBcg.jpeg'


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