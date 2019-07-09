# Navbar

> read about css variables

First we create `css folder` where we create `ccs.module` file. Then import it in the `Navbar` component. 

**Navbar**

```jsx
import React from 'react'
import styles from '../css/navbar.module.css'

const Navbar = () => {
  return (
      <div>
          <p>My Navbar</p>
      </div>
  )
}

export default Navbar;
```

Then we'll also need `font awesome icon`, so we need to import it as well. 

**Navbar**

```jsx
import React from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"

const Navbar = () => {
  return (
      <div>
          <p>My Navbar</p>
      </div>
  )
}

export default Navbar;
```
For our Navbar we'll also need `links` and `social icons`. Let's import them also. 

**Navbar**

```jsx
import React from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'

const Navbar = () => {
  return (
      <div>
          <p>My Navbar</p>
      </div>
  )
}

export default Navbar;
```

The last one will be the `logo`. The most straightforward way of getting the images in `Gatsby` will be importing it in the `js file` and then using it in the `component`.

**Navbar**

```jsx
import React from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import logo from '../images/logo.svg'

const Navbar = () => {
  return (
      <div>
          <p>My Navbar</p>
      </div>
  )
}

export default Navbar;
```

Now we can start working on our logic. 

For the toggling we'll use `React hooks`. Let's import `{useState}` and setup our `toggling function`. 

**Navbar**

```jsx
import React, {useState} from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import logo from '../images/logo.svg'

const Navbar = () => {

  const [isOpen, setNav] = useState(false)

  const toggleNavbar = () => {
    setNav(isOpen => !isOpen)
  }

  return (
      <div>
          <p>My Navbar</p>
      </div>
  )
}

export default Navbar;
```

Now we start working on jsx.

**Navbar**

```jsx
import React, {useState} from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import logo from '../images/logo.svg'

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
          </div>
      </nav>
  )
}

export default Navbar;
```

Now, when we have our `logo` and the `button` that toggles the `navbar`, after the `div` with the `className` "navHeader" we wanna setup `nav links`. It will be an unordered list. And here we'll not be typing the simple `className` cos we are doing the toggling. This is gonna be the case where we do wanna add two classes: 

- one is: 
```css
.nav-links {
  list-style-type: none;
  transition: var(--mainTransition);
  height: 0;
  overflow: hidden; 
}
```
- and the second one - depending on the `value` in the `state` (isOpen), we'll either use

```css
.show-nav {
  height: 216px;
}
```
Or we'll gonna hide it. 

So, we'll use `ternary operator` here. If `isOpen` is `true` then we'll render two classes, if it will be `false` then only one class will be rendered. For that we'll use `template literals` and access style classes as `variables`. 

**Navbar**
```jsx
import React, {useState} from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import logo from '../images/logo.svg'

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
              <ul className={isOpen?`${styles.navLinks} ${styles.showNav}` : `${styles.navLinks}`}>

              </ul>
          </div>
      </nav>
  )
}

export default Navbar;
```
Then within the unordered list we wanna render two things: `links` and `social icons`. We need to access in this case java script, then use `map()` method, and in the `callback function` we'll be accessing two things: one will be the `item` and the second one - the `index`. We'll have `<li>` where we'll render our `<Link/>` with the `to` prop, within the `to prop` we wanna access the value - `{item.path}`. 

**Navbar**
```jsx
import React, {useState} from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import logo from '../images/logo.svg'
import {Link} from 'gatsby'


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
                    <Link to={item.path}>{item.text}</Link>
                  </li>
                  
                ))}
              </ul>
          </div>
      </nav>
  )
}

export default Navbar;
```

Last thing - after the `links` we wanna get our `social media icons`. For that we'll create another `div`, inside with the links. In this case it will be a simple `link`, not the `<Link/>` component, the reason for that is  - this well be an `external link`, it will be leaving our page. In the `link` we also need to add a `target` cos we wanna open it in a new page, cos that way the user will not leave our page. Also not to have a security risk we'll add `rel="noopener noreferrer"` for the `target`. 

**Navbar**
```jsx
import React, {useState} from 'react'
import styles from '../css/navbar.module.css'
import {FaAlignRight} from "react-icons/fa"
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import logo from '../images/logo.svg'
import {Link} from 'gatsby'


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
                    <Link to={item.path}>{item.text}</Link>
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

Well we still cannot toggle. And the reason is simple - in our css `nav-links` class we shoul have: `height:0, overflow: hidden`. 
