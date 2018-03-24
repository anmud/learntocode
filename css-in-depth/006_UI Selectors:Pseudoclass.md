**A pseudo-class is used to define a special state of an element.**

For example, it can be used to:

* Style an element when a user mouses over it
* Style visited and unvisited links differently
* Style an element when it gets focus

In `html` you can have elements that are enable or disabled, you can have elements that are checked or not checked. 

Based on current state of UI

  `:enabled`

  `:disabled`

  `:checked`

  `:indeterminate` (Level 4)

Example:

Any label (+  means immediately following) that comes immediately after the checked input of type checkbox should have red color. 

```css
input[type=checkbox]:checked + label {
  color: red;
}
```
![checked](./checked.png)

And because i was thinking about accessibility and included a label i would actually have to check on a checkbox  - and i can check on a label and it will toggle on and off. That's toggling the checkbox which is activating the CSS. 

CSS updates immediately, we just update the UI feature. 

The UI features that we have:

:default

:valid

:invalid

:required
:optional

:in-range
:out-of-range

:read-only
:read-write

:placeholder-shown

:user-error or :user-invalid
