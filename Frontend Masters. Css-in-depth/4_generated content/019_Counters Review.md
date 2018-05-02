# Review

### Example 1
```css
body {counter-reset: invalidCount;}
:invalid {
  background-color: pink;
  counter-increment: invalidCount;
}
p:before {
  content: "You have " 
      counter(invalidCount) " invalid entries";
}
```
![counter_review](../counter_review.png)

### Example 2

```css
body { counter-reset: pagecount; }
p { 
	counter-increment: pagecount;
}
p:after { color: magenta;
  content: "" counter(pagecount);
}
```
![counter_review_example2](../counter_review_example2.png)

