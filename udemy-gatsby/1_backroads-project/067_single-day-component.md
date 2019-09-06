# Single Day Component

Let's finish our `single day component`. For this component we'll import hooks, namely `useState`. Well, we remember that we are passing two props: `day` and `info` from our template component - and first of all we'll destructure them for the component.   

**Day**

```js
import React, {useState} from 'react'
import {FaAngleDown} from "react-icons/fa"
import styles from "../../css/day.module.css"


const Day = ({day, info}) =>{
  return (
     <article className={styles.day}>
      <h4>
      {day}
          <button className={styles.btn}>
              <FaAngleDown/>
          </button>
      </h4>
      <p>{info}</p>
     </article>
  )
}

export default Day;
```

Now we need to add some functionality - part of the information will be hidden by default and by clicking a button we'll be able to see it. For that purpose we'll use `useState` hook and the `&& operator` - we'll gonna check that if the variable by the name of `showInfo` is true then we would want to render whatever is on the other side of the operator. 

`{showInfo &&   <p>{info}</p> }`

**Day**

```js
import React, {useState} from 'react'
import {FaAngleDown} from "react-icons/fa"
import styles from "../../css/day.module.css"


const Day = ({day, info}) =>{

const [showInfo, setInfo] = useState(false)

  return (
     <article className={styles.day}>
      <h4>
      {day}
          <button className={styles.btn}>
              <FaAngleDown/>
          </button>
      </h4>
      {showInfo &&  <p>{info}</p> }
    
     </article>
  )
}

export default Day;
```


Next we need to setup a function that will control our state and we'll use a button.  

```js
import React, {useState} from 'react'
import {FaAngleDown} from "react-icons/fa"
import styles from "../../css/day.module.css"


const Day = ({day, info}) =>{

const [showInfo, setInfo] = useState(false)

const toggleInfo = () => {
    setInfo(showInfo => !showInfo)
}


  return (
     <article className={styles.day}>
      <h4>
      {day}
          <button className={styles.btn} onClick={toggleInfo}>
              <FaAngleDown/>
          </button>
      </h4>
      {showInfo &&   <p>{info}</p> }
    
     </article>
  )
}

export default Day;
```

