# Transition Link Plugin

Let's add a transition as we are going from page to page. In order to set it up we need to setup the plugin - `"gatsby-plugin-transition-link"` - `npm i gatsby-plugin-transition-link`. 

We need to add it then to `gatsby-config.js` file. 

**gatsby-config.js**

```jsx
module.exports = {
    plugins: [
      `gatsby-plugin-transition-link`
    ]
];
```

For now we need as well to install one more package - `"AniLink"`. And now we need to restart the server. 

Well, actually now we have two options: we can use the `TransitionLink` or `AniLink`. For now we will use `AniLink` cos it's much easier for now - we just need to pass a `prop`. Anyway you can use `TransitionLink` in the future - it gives a lot of oppotrunities. 

Let's start with our `Navbar` cos we have bunch of links there. First we'll import `AniLink` - `import AniLink from "gatsby-plugin-transition-link/AniLink"`. Actually what we need to do is to replace all simple `Links` with the `AniLink`. 

**Navbar.js**

```jsx
import React, {useState} from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import logo from '../images/logo.svg'
//import {Link} from 'gatsby'
import AniLink from "gatsby-plugin-transition-link/AniLink";



const Navbar = () => {

  const [isOpen, setNav] = useState(false)

  console.log(isOpen)

  const toggleNav = () => {
    setNav(isOpen => !isOpen)
  }

  return (
      <nav className={styles.navbar}>
          <div className={styles.navCenter}> 
              <div className={styles.navHeader}>
                  <img src={logo} alt="backroads logo"/>
                  <button type="button" className={styles.logoBtn} onClick={toggleNav}>
                    <FaAlignRight className={styles.logoIcon}/>
                  </button>
              </div>
              <ul className={
                isOpen
                ?`${styles.navLinks} ${styles.showNav}` 
                : `${styles.navLinks}`
                }>
                {links.map((item, index) => (
                
                  <li key={index}>
                    <AniLink to={item.path}>{item.text}</AniLink>
                  </li>
                  
                ))}
              </ul>
              <div className={styles.navSocialLinks}>
                 {socialIcons.map((item, index) => (
                   <a key={index} href={item.url} target="_blank" rel="noopener noreferrer">{item.icon}</a>
                 ))}
              </div>
          </div>
      </nav>
  )
}

export default Navbar;
```

There are transitions options: we can choose the one we want and pass ia as a `prop`.


**Navbar.js**

```jsx
import React, {useState} from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import logo from '../images/logo.svg'
//import {Link} from 'gatsby'
import AniLink from "gatsby-plugin-transition-link/AniLink";



const Navbar = () => {

  const [isOpen, setNav] = useState(false)

  console.log(isOpen)

  const toggleNav = () => {
    setNav(isOpen => !isOpen)
  }

  return (
      <nav className={styles.navbar}>
          <div className={styles.navCenter}> 
              <div className={styles.navHeader}>
                  <img src={logo} alt="backroads logo"/>
                  <button type="button" className={styles.logoBtn} onClick={toggleNav}>
                    <FaAlignRight className={styles.logoIcon}/>
                  </button>
              </div>
              <ul className={
                isOpen
                ?`${styles.navLinks} ${styles.showNav}` 
                : `${styles.navLinks}`
                }>
                {links.map((item, index) => (
                
                  <li key={index}>
                    <AniLink fade to={item.path}>{item.text}</AniLink> // add prop here
                  </li>
                  
                ))}
              </ul>
              <div className={styles.navSocialLinks}>
                 {socialIcons.map((item, index) => (
                   <a key={index} href={item.url} target="_blank" rel="noopener noreferrer">{item.icon}</a>
                 ))}
              </div>
          </div>
      </nav>
  )
}

export default Navbar;
```

Now, let's start working with the other two pages where we'll use the `AniLink` - `404 page` and what we are navigating from the `home page` to the `tours page` using the `explore tours button`. We also will change the `Link` to `AniLink` and add `fade` prop. 

