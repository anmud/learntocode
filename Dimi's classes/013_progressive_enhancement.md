# Progressive Enhancement

## Enchiridion of HTML/CSS

> **HTML** is about dividing content into blocks (`<div>, <main>, <aside>`), giving these blocks meaning (`<p>,<h1>, <article>`) and using browser API to perform some actions (`<form>, <input>, <textarea>`). 
> **CSS** is about styling these blocks! HTML - markups the text and CSS - styles the text.

> Use **Progressive Enhancement** while designing for web: 
>1) Identify core functionality. 
>2) Make that functionality available using the simplest possible technology. 
>3) Enhance! 

---
## Progressive Enhancement for building Web Apps

1. Identify core functionality:
..* Define the core functionality e.g. slack - display/send/receive a message More examples

..* Define the lowest common denominator a baseline device (e.g. mobile, tablet, desktop, kindle, alexa)

..* Define the initial data model and make it visible <pre>JSON.stringify()</pre>

..* Design basic structure with <div>'s and HTML5 sematic blocks for a baseline device