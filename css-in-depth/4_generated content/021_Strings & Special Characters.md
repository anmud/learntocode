We need to have `content` attribute and have something in it, or an empty string with the quotes `" "`, etc.

### Syntax

```
 element:before {
  content: "REQUIRED";
 }
 ```

 ```
  element:before {
    content: '';                  /* empty */
    content: " (.pdf) ";          /* any text */
    content: "\2603";             /* unicode */
    content: " (" attr(href) ")"; /* attributes */
    content: counter(name);
        counter-increment: name;  /* counters */
 }
 ```
 