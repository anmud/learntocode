# The `:lang()` pseudo-class 

The `:lang()` selector is used to select elements with a lang attribute with the specified value.

CSS 2.1

```css
html[lang|="en"] /*says is that attribute present on this element, actually here in the whole document*/
p:lang(en) /*is this the language of this element at this time right now*/
```
CSS Selectors Level 4

```css
:lang(*-ch)
:dir(ltr|rtl) /*direction - left-to-right or right-to-left*/
```
:dir => FF only, :lang(*-ch) => none