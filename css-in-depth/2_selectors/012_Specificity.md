# Specificity 

`X-0-0` the number of ID selectors

`0-Y-0` the number of class selectors, attributes selectors and pseudo-classes

`0-0-z` the number of type selectors and pseudo-elements

`*, +, >, ~`  universal selectors and combinators don't increase specificity 

`:not()` negation-selector has no value, argument increases it's specificity 

Calculating exact specificity values seems tricky at first. You need to:

* count the number of ID selectors in the selector (= A)

* count the number of class selectors, attribute selectors, and pseudo-classes in the selector (= B)

* count the number of type selectors and pseudo-elements in the selector (= C)

* ignore the universal selector

Complex and combinator selectors, of course, give us higher specificity values. Let’s look at an example. Consider the following CSS:

```css
ul#story-list > .book-review {
    color: #0c0;
}

#story-list > .book-review {
    color: #f60;
}
```

These two rule sets are similar, but they are not the same. The first selector, `ul#story-list > .bookreview`, contains a type selector (ul), an ID selector, (#story-list), and a class selector (.bookreview). It has a specificity value of 1,1,1. The second selector, `#story-list > .book-review` only contains an ID and a class selector. Its specificity value is 1,1,0. The higher specificity of the former means that those elements with a `.book-review` class will be green rather than orange.

Pseudo-classes such as `:link` or `:invalid` have the same level of specificity as class selectors. Both `a:link` and `a.external` have a specificity value of 0,1,1. Similarly, pseudo-elements such as `::before` and `::after` are as specific as type or element selectors. In cases where two selectors are equally specific, the cascade kicks in. Here’s an example:

```css
a:link {
    color: #369;
}
a.external {
    color: #f60;
}
```
If we applied this CSS, every link would be slate blue except for those with class="external" applied. Those links would be orange instead.

[Here you can find CSS Specificity with icons](http://cssspecificity.com/)

[Here you can find the CSS calculator](https://specificity.keegan.st/)