# Footer

First we need to import all things we need: styles, links, social icons, react-icons and the `<Link/>` fro `gatasy`. 

**Footer**

```jsx
import React from 'react'
import styles from '../css/footer.module.css'
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import {Link} from 'gatsby'
import {FaRProject} from 'react-icons/fa'

const Footer = () => {
  return (
      <div>
          <p>My Footer</p>
      </div>
  )
}

export default Footer;
```

Now we can start working with the jsx. We'll have there the `div` with `link`, then `social icons` and little bit of `copyright`.

**Footer**
```jsx
import React from 'react'
import styles from '../css/footer.module.css'
import links from '../constants/links'
import socialIcons from '../constants/social-icons'
import {Link} from 'gatsby'
import {FaRProject} from 'react-icons/fa'

const Footer = () => {
  return (
      <footer className={styles.footer}>
        <div className={styles.links}>
        {links.map((item, index) => (
          <Link key={index} to={item.path}>{item.text}</Link>
        ))}
        </div>
        <div className={styles.icons}>
          {socialIcons.map((item, index) => (
            <a key={index} href={item.url} target="_blank" rel="noopener noreferrer">{item.icon}</a>
          ))}
        </div>
        <div className={styles.copyright}>
          copiright &copy; backroads travel company {new Date().getFullYear()} all rights reserved
        </div>
      </footer>
  )
}

export default Footer;
```
