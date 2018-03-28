# `open-quote` `close-quote`

**"As she lay her head on the pillow, she whispered in my ear, 'Did you feed the cats?'"**

**«Quand sa tête reposa finalement sur l'oreiller, elle me murmura à l'oreille, ’As-tu nourri les chats?’»**
**HTML**
```html
<p lang="en-us"><q>As she lay her head on the pillow, she whispered in my ear, <q>Did you feed the cats?</q></q></p>

<p lang="fr-fr"><q>Quand sa tête reposa finalement sur l'oreiller, elle me murmura à l'oreille, <q>As-tu nourri les chats?</q></q>
```
**CSS**
```css
/* Specify pairs of quotes for two levels in two languages */
:lang(en) > q { quotes: '"' '"' "'" "'" }
:lang(fr) > q { quotes: "«" "»" "’" "’" }

/* Insert quotes before and after Q element content */
q::before { content: open-quote }
q::after  { content: close-quote }

p {
  font-size: 2em;
  cont-family: georgia;
}
```

Here when you suppose to have a quote, you can say the first quote at the opening is this type of qute and then at the end is that type of quote, but if it's nested give me the options number 3 and number 4. 

#  `no-close-quote`

"As she lay her head on the pillow, she whispered in my ear, 'Did you feed the cats?'

"This wasn't the first time time she woke me up this way. Nor was it the most annoying.

"Usually, she doesn't whisper, and rather jolts me awake with, 'Did you check all the doors?'"

**HTML**
```html
<article  lang="en-us">
  <p>As she lay her head on the pillow, she whispered in my ear, <q>Did you feed the cats?</q>

<p>This wasn't the first time time she woke me up this way. Nor was it the most annoying.</p>
  
<p>Usually, she doesn't whisper, and rather jolts me awake with, <q>Did you check all the doors?</p>
</article>
```
**CSS**
```css
:lang(en) q { quotes: '"' '"' "'" "'" }
:lang(fr) q { quotes: "«" "»" "’" "’" }

/* Insert quotes before and after Q element content */
p::before { content: open-quote }
p::after { content: no-close-quote }
p:last-of-type::after  { content: close-quote }

p {
  font-size: 2em;
  cont-family: georgia;
}
```
# Attribute values as content

There are [local examples](https://estelle.github.io/cssmastery/generated/files/02_generatedtext.html), or you can search [Google](lmgtfy.com/?q=css+generated+content+attributes).

```css
a[href^=http]:hover {
   position: relative;
}
a[href^=http]:hover:after {
   content: attr(href);
   position: absolute;
   top: 1em;
   left: 0;
   background-color: black;
   color: white;
   padding: 3px 5px;
   line-height:1;
} 
```
