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

1. **Identify core functionality:**
   - Define the core functionality (e.g. "slack" - display/send/receive a message)
   - Define the lowest common denominator a baseline device (e.g. mobile, tablet, desktop, kindle, alexa)
   - Define the initial `data model` and make it visible `<pre>JSON.stringify()</pre>`
   - Design basic structure with `<div>`'s and HTML5 sematic blocks for a baseline device
2. **Make the core functionality available using the SIMPLEST POSSIBLE TECHNOLOGY.**
   - Add behavior (scripts, css hover, onclick(), oninput() etc.)
   - Add backend (lambda, database, gateway, queues etc.)
3. **Enhance**
   - Add layout markup and stylesheets for structural layout `.container` with breakpoints
   - Add presentational stylesheets for a baseline device
   - Add presentational stylesheets for other devices

## Progressive Enhancement for building Propducts

1. Identify core functionality.
2. Make that functionality available using the simplest possible technology.
3. Enhance!

---

1). It’s our job to tell the browser, in a way that it can understand, what each of these elements mean and how they fit together semantically. If this is not done, then our site will appear as a clump of single text.

   - Here is a simple text that can be also shown in the browser, but as a chunk of text

```
"Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit..."
"There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain..."
```

   - Here we mark the words with HTML, so a Browser can understand the structure

```html
<h1>"Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit..."</h1>
<p>"There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain..."</p>
```

2). Before creating any kind of web page, it’s a good idea to divide the content into smaller components by their importance.

```
We're looking for an HTML and CSS developer
[image]
For our client, The Cat Factory, we need a skilled web developer in HTML and CSS. We offer a competitive salary, a bag of cat food and toys.
Don't wait, apply now! Our crazy team is waiting for your right meow!
```

The key problem is that we’ve created a website with only plain text. A web browser cannot understand how to display a page properly with only plain text — it doesn’t know which part of the text should be the title or which part should be a picture. In order to display the page properly, we need to define each element by the function of the text and pass this information to the browser.

```html
<h1>We're looking for an HTML and CSS developer</h1>
<img src"images/white-cat.jpg">
<p>For our client, The Cat Factory, we need a skilled web developer in HTML and CSS. We offer a competitive salary, a bag of cat food and toys.</p>
<p>Don't wait, apply now! Our crazy team is waiting for your right meow!</p>
```
As you can see, there are special markings within the text. `Hypertext Markup Language`, and is the primary markup language for displaying information for a web browser. In simpler terms, it’s a language that uses “tags” to mark text, so that you can describe the text to your browser.

3). Attributes are modifiers in HTML, and are always written next to the tag, between the <> enclosure. Attributes have the following template when writing code. tag attribute="value"
