# Adding Media Queries for medium and small screens

Now we gonna add some `CSS` into our `html email`. Let's start with `@media only screen and(max-width:660px) {}` - that's gonna be a medium screen. 

Since we are not adding a `min-width`, any rules that we assign inside of `660` will also be triggered inside of the `510`; and all of the elements in inline styles of the `html` in general will be applied to three of these as well.  So with these `media queries` we gonna be overriding, only what needs to be changed for `medium screens` at `660` and small screens at `510`. 

### HTML
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Our Vineyard</title>
		<style type="text/css">
			@media only screen and (max-width: 660px) {

			}
			@media only screen and (max-width: 510px )
		</style>
	</head>	
    .......
    ......
    ......
```
The first `rule` we gonna create for the `660`. This rule gonna target the `table `element with the `class` of "container" . We need to add the `!imortant` flag for the rule. This `flag` overwrites the `width` attribute we placed on the `table tag` itself in our `html body`. Normally, elements inline styles that are placed on the individual elements will overwrite CSS rules, so we need the `important flag`. 

And considering we need to use a lot of `inline styles` and `element properties` for older `html email clients`, we gonna need to use the `important flag` to overwrite some of these properties for the `responsiveness` of our project. 

Let's add two more rules to change the sizing for the small screens, we'll target the `table with the class container` and also `td` inside this table container where we gonna remove the `border`. Once we get under the `510` width we gonna have `100%` width. So. once we get under `510` we gonna have the design stretched to the `full width` and we gonna get rid of the border that we see for our large and medium screens. 

### HTML
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Our Vineyard</title>
		<style type="text/css">
			@media only screen and (max-width: 660px) {
              table.container{
				  width: 480px !important;
			  }
			}
			@media only screen and (max-width: 510px ){
				table.container{ width: 100% !important;}         /*full width under 510*/
				table.container td {border: none !important;}      /*no border*/
			}
		</style>
    </head>	
```
Let's come back to the `660` size, we gonna target the `image` in the `logo row` : we'll set display to none; then we gonna target the `td` itself: here we gonna set the background color to white and the url for the smaller image. What this is gonna do - is hide the `logo graphic` and place the background graphic at the `td` with th emedium-size logo.  

### HTML
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Our Vineyard</title>
		<style type="text/css">
			@media only screen and (max-width: 660px) {
              table.container {width: 480px !important; }
			  td.logo img {display: none;}
			  td.logo {background: #fff url(images/logo_medium.gif) no-repeat 10px 10px; height: 45px }
			}
			@media only screen and (max-width: 510px ){
				table.container{ width: 100% !important;}
				table.container td {border: none !important;}
			}
		</style>
    </head>	
```
Inside the smaller screen area we don't need to turn the `logo` off because we are are compoundin this, since we don't have the `min width`. We will target the `td` with the `logo` class and set the smaller image. 

### HTML
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Our Vineyard</title>
		<style type="text/css">
			@media only screen and (max-width: 660px) {
              table.container {width: 480px !important; }
			  td.logo img {display: none;}
			  td.logo {background: #fff url(images/logo_medium.gif) no-repeat 10px 10px; height: 45px }
			}
			@media only screen and (max-width: 510px ){
				table.container{ width: 100% !important;}
				table.container td {border: none !important;}
				td.logo {background: #fff url(images/logo_small.gif) no-repeat center 10px; height: 32px}
			}
		</style>
    </head>
``` 