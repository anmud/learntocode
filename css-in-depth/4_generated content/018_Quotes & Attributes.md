### Example

```css
/* Specify pairs of quotes for two levels in two languages */
:lang(en) > q { quotes: '"' '"' "'" "'" }
:lang(fr) > q { quotes: "«" "»" "’" "’" }

/* Insert quotes before and after Q element content */
q::before { content: open-quote }
q::after  { content: close-quote }
```

"As she lay her head on the pillow, she whispered in my ear, 'Did you feed the cats?'"

«Quand sa tête reposa finalement sur l'oreiller, elle me murmura à l'oreille, ’As-tu nourri les chats?’»

Here when you suppose to have a quote, you can say the first quote at the opening is this type of qute and then at the end is that type of quote, but if it's nested give me the options number 3 and number 4. 

