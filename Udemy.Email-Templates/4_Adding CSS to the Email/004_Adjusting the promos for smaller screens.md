# Adjusting the promos for smaller screens

Let's set some rules to target the `promos row`. First we'll target the `table` inside of the `<td>` promos; then the `headings` inside; images, then `<td>` inside the `promo1` and  `promo_2`. 

### HTML head
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
			  td.headline {padding: 5px 0px 0px 30px !important}
			  td.headline h1 {font-size: 28px !important}

			  td.banner img {display: none}
			  td.banner {width: 480px; height: 150px; background: url(images/banner_medium.jpg) no-repeat 0px 0px;}
              td.content {padding-bottom: 30px !important; background-image: url(images/banner_medium_ghost.jpg) no-repeat !important;}
			  td.content table.button {width: auto;}
			  td.content table.button td a {font-size: 14px !important}
			  td.promos table {width: 200px !important;}  /* change rules for the promos table*/
			  td.promos table td h3 {margin-bottom: 8px;}   /* change rules for the promos headings*/
			  td.promos table td img {display: none;}    /* change rules for the promos image*/
			  td.promos table.promo_1 td {background: url(images/promo_1_medium.jpg) no-repeat 0px 0px; padding: 100px 0px 0px 0px;}  /* change rules for the promo_1*/
			  td.promos table.promo_2 td {background: url(images/promo_2_medium.jpg) no-repeat 0px 0px; padding: 100px 0px 0px 0px;}  /* change rules for the promo_2*/
			}

			@media only screen and (max-width: 510px ){
				table.container{ width: 100% !important;}
				table.container td {border: none !important;}
				td.logo {background: #fff url(images/logo_small.gif) no-repeat center 10px; height: 32px}
				td.headline h1 {font-size: 24xp !important; text-align: center;}
				td.banner {height: 115px; background: url(images/banner_small.jpg) no-repeat right 0px;}
				td.content {line-height: 20px !important; padding-bottom: 10px !important; background: #f5f2e5  
				url(images/banner_small_ghost.jpg) no-repeat right 0px !important}
				td.footer {padding: 20px 30px !important}
			}
		</style>
    </head>	
```
Next, let's add some rules for the smaller screens. Here in the rules we'll use `clear rule` - when for some reasons a `table` isn't resized to 100% we can be asure the `table` will have the `clear:left`, so will align on the left hand side with the table above it. 

### HTML head
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
			  td.headline {padding: 5px 0px 0px 30px !important}
			  td.headline h1 {font-size: 28px !important}

			  td.banner img {display: none}
			  td.banner {width: 480px; height: 150px; background: url(images/banner_medium.jpg) no-repeat 0px 0px;}
              td.content {padding-bottom: 30px !important; background-image: url(images/banner_medium_ghost.jpg) no-repeat !important;}
			  td.content table.button {width: auto;}
			  td.content table.button td a {font-size: 14px !important}
			  td.promos table {width: 200px !important;}
			  td.promos table td h3 {margin-bottom: 8px;}
			  td.promos table td img {display: none;}
			  td.promos table.promo_1 td {background: url(images/promo_1_medium.jpg) no-repeat 0px 0px; padding: 100px 0px 0px 0px;}
			  td.promos table.promo_2 td {background: url(images/promo_2_medium.jpg) no-repeat 0px 0px; padding: 100px 0px 0px 0px;}
			}

			@media only screen and (max-width: 510px ){
				table.container{ width: 100% !important;}
				table.container td {border: none !important;}
				td.logo {background: #fff url(images/logo_small.gif) no-repeat center 10px; height: 32px}
				td.headline h1 {font-size: 24xp !important; text-align: center;}
				td.banner {height: 115px; background: url(images/banner_small.jpg) no-repeat right 0px;}
				td.content {line-height: 20px !important; padding-bottom: 10px !important; background: #f5f2e5  
				url(images/banner_small_ghost.jpg) no-repeat right 0px !important}
				td.footer {padding: 20px 30px !important}
				td.promos table.promo_1 {width: 100% !important;} /* change rules for the promo_1 table*/
				td.promos table.promo_1 td {background: url(images/promo_1_small.jpg) no-repeat 0px 40px; padding: 20px 0px 40px 110px;} /* change rules for the promo_1 td*/
				td.promos table.promo_2 {width: 100% !important;} /* change rules for the promo_2 table*/
				td.promos table.promo_2 td {background: url(images/promo_2_small.jpg) no-repeat 0px 20px; padding: 0px 0px 0px 110px; clear: left;} /* change rules for the promo_2 td*/
			}
		</style>
    </head>	
```