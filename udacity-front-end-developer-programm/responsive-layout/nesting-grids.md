# Building Responsive Layouts with Flexbox & Grid

One of the most useful features of CSS grid is that you can easily nest grids inside each other to create elegant, complex layouts. To nest CSS grids simply set the display property of the container element to grid and then select the child grid item you want to make the nested grid and set the display property of that element to grid as well! The same grid rules you’ve been learning still apply! Easy as that!

Nesting CSS grids is simple and can be done simply by using the display:grid rule for both a parent and child element.

Here is how that could look with real code:

```css
.container {
  display:grid;
  // ...
}

#one {
  display:grid
}
```

**html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Exercise 1</title>
    <meta
      content="width=device-width, initial-scale=1, maximum-scale=1"
      name="viewport"
    />
    <link rel="stylesheet" href="css/style.css">
  </head>

  <body>
  <div class = "container">
    <div class="header box">Header</div>
    <div class="sidebar box"><h1>Blog Posts</h1><a href="post.html">Most Recent Post</a></div>
    <div class="content box">
      <div class="nestedGrid">
        <div id="one" class="phpo box">
          <h1>your favorite day of the week</h1>
        </div>
         <div id="two" class="phpo box">
          <h1> your favorite season</h1>
        </div>
        <div id="three" class="phpo box">
          <h1> your nickname</h1>
        </div>
        <div id="four" class="phpo box">
          <h1> your favorite ice cream flavor</h1>
        </div>
      </div>

    </div>
    <div class="footer box">Footer</div>
  </div>
  </body>
</html>
```

**css**

```css
.container{
  display:grid;
  grid-template-columns: 300px 300px 300px;
  grid-template-rows: 250px 600px;
  /* grid-template-columns: repeat(3, 1fr); */
  /* Initially each element has its own row for small screens */
  grid-template-areas: 
  "hd"
  "sd"
  "main"
  "ft";
  border: 2px solid yellow;
}
/* add css for nested grid here */
.box{
    border: 1px solid red;
    background: #F8FA9D;
    }
  .header{
    /* row start/column start/ row end/ column end */
    grid-area:hd;
  }
  .footer{
    grid-area: ft;  
  }
  .sidebar{
    grid-area: sd;
  }
  .content{
    grid-area: main;
  }

.nestedGrid{
  display: grid;
  grid-template-columns: 50% 50%;
  grid-template-rows: 50% 50%;
}

/* If Screen Is Wide Enough */
@media(min-width:900px){
.container{
      display:grid;
      grid-template-columns: 300px 300px 300px;
      grid-template-rows: 250px 600px;
      grid-template-areas: 
      "hd hd hd hd hd hd hd hd"
      "sd sd main main main main main main"
      "ft ft ft ft ft ft ft ft";
      border: 2px solid red;
  }
}
```