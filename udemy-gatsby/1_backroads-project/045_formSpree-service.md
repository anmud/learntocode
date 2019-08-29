# FormSpree Service

Now we need to take a look at how we can collect the values that the user will be using. To deal with it we'll use the service called (FormSpree)[https://formspree.io/]. We'll add the `action` attribute with the `value` of our email as well as the ` POST method` for our `form`.

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
            <form 
            action="https://formspree.io/anmud@list.ru" 
            method="POST"
            className={styles.form}>
              <div>
                  <label htmlFor="name">name</label>
                  <input type="text" name="name" id="name" className={styles.formControl} placeholder="ana mo"/>
              </div>
              <div>
              <label htmlFor="email">email</label>
                  <input type="email" name="email" id="email" className={styles.formControl} placeholder="email@email.com"/>
              </div>
              <div>
              <label htmlFor="message">message</label>
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

Now we would like to test it, and what is really awesome about this service - we can test it on the `local server`. WE just need to enter the data in our `form`. For the first time when we'll test the form `FormSpree` will also ask us to activate the `form`. 
