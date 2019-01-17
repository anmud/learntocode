# Adding HTML5 video into email

Let's take a look at how we can incorporate HTML5 video into an email. The first we gonna do is to remove the `promos` and replace them with video. Once they are remove we gonna add an `video` tag, add some styling and `video poster`; set `controls attribute`. Inside the `video tag` we'll add a `source` tag which will point to the `video file`. Next we'll put some `html content` inside that will be seen by `email clients` that don't understand the `video tag`. So, we'll add a standart `anchor link` and put the URL to your website, specifically to html file, that's using the same video. Inside the `anchor tag ` we'll put the `image` of that same `poster frame`, for users who don't see the video in the `email client` that have the same `poster frame` they will be linked to a `website` that has the same video. 

### HTML
```html
<tr><!--promos row-->
						<td valign="top" bgcolor="#f5f2e5" class="promos" style="padding: 10px 30px 25px 30px;  
						border-right:1px solid #dbc064; border-left:1px solid #dbc064;  
						background-color: #f5f2e5; font-family: Arial, Helvetica, sans-serif;">
                           <video width="570" height="428" poster="video/our_vineyard.jpg" controls="controls">
                            <source src="video/our_vineyard.mp4" type="video/mp4">
                            <a href="http://yoursite.com/video.html">
                                <img src="video/our_vineyard.jpg">
                            </a>
                        </video>
						</td>
                    </tr>
``` 

We need to add some `CSS rules` to make sure this `video object` is `responsive`. Let's first go to our `media queries` for the medium sized screens. First we'll target the `video tag` and then the `image` inside of the video, even though we shouldn't see this for email clients that support video. 

### HTML head
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Our Vineyard</title>
		<style type="text/css">
		    @import url('https://fonts.googleapis.com/css?family=Parisienne');

		     body {margin: 0; padding: 0;}

			@media only screen and (max-width: 660px) {
              table.container {width: 480px !important; }
			  td.logo img {display: none;}
			  td.logo {background: #fff url(images/logo_medium.gif) no-repeat 10px 10px; height: 45px; }
			  td.headline {padding: 5px 0px 0px 30px !important;}
			  td.headline h1 {font-size: 28px !important;}

			  td.banner img {display: none}
			  td.banner {width: 480px; height: 150px; background: url(images/banner_medium.jpg) no-repeat 0px 0px;}
              td.content {padding-bottom: 30px !important; background-image: url(images/banner_medium_ghost.jpg) no-repeat !important;}
			  td.content table.button {width: auto;}
			  td.content table.button td a {font-size: 14px !important;}
			  td.promos table {width: 200px !important;}
			  td.promos table td h3 {margin-bottom: 8px;}
			  td.promos table td img {display: none;}
			  td.promos table.promo_1 td {background: url(images/promo_1_medium.jpg) no-repeat 0px 0px; padding: 100px 0px 0px 0px;}
			  td.promos table.promo_2 td {background: url(images/promo_2_medium.jpg) no-repeat 0px 0px; padding: 100px 0px 0px 0px;}
			  td.callout table {width: 50% !important; margin-bottom: 40px;}
			  td.callout table img {display: none;}
			  td.callout table br {display: none;}
			  td.callout table a {display: block; margin-top: 10px;}
			  td.callout table td {background-size: 65px 65px;}
			  td.callout table.callout_1 td {padding: 0px 30px 0px 60px !important; background: url(images/icon_grapes.gif) no-repeat 0px -13px;}
			  td.callout table.callout_2 td {padding: 0px 20px 0px 60px !important; background: url(images/icon_bottle.gif) no-repeat 10px -3px;}
			  td.callout table.callout_3 td {padding: 0px 30px 0px 60px !important; background: url(images/icon_basket.gif) no-repeat 0px -13px; clear: left;}
			  td.callout table.callout_4 td {padding: 0px 20px 0px 60px !important; background: url(images/icon_camera.gif) no-repeat 10px -23px;}
               
              video {width: 416px !important; height: 312px !important;}    /*add video rules*/
              video img {width: 416px !important; height: 312px !important;}  /*add video rules*/

			}
            ......
```

Next, let's add rules for the small screens. 

### HTML head

```html
	<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<title>Our Vineyard</title>
		<style type="text/css">
		    @import url('https://fonts.googleapis.com/css?family=Parisienne');

		     body {margin: 0; padding: 0;}

			@media only screen and (max-width: 660px) {
              table.container {width: 480px !important; }
			  td.logo img {display: none;}
			  td.logo {background: #fff url(images/logo_medium.gif) no-repeat 10px 10px; height: 45px; }
			  td.headline {padding: 5px 0px 0px 30px !important;}
			  td.headline h1 {font-size: 28px !important;}

			  td.banner img {display: none}
			  td.banner {width: 480px; height: 150px; background: url(images/banner_medium.jpg) no-repeat 0px 0px;}
              td.content {padding-bottom: 30px !important; background-image: url(images/banner_medium_ghost.jpg) no-repeat !important;}
			  td.content table.button {width: auto;}
			  td.content table.button td a {font-size: 14px !important;}
			  td.promos table {width: 200px !important;}
			  td.promos table td h3 {margin-bottom: 8px;}
			  td.promos table td img {display: none;}
			  td.promos table.promo_1 td {background: url(images/promo_1_medium.jpg) no-repeat 0px 0px; padding: 100px 0px 0px 0px;}
			  td.promos table.promo_2 td {background: url(images/promo_2_medium.jpg) no-repeat 0px 0px; padding: 100px 0px 0px 0px;}
			  td.callout table {width: 50% !important; margin-bottom: 40px;}
			  td.callout table img {display: none;}
			  td.callout table br {display: none;}
			  td.callout table a {display: block; margin-top: 10px;}
			  td.callout table td {background-size: 65px 65px;}
			  td.callout table.callout_1 td {padding: 0px 30px 0px 60px !important; background: url(images/icon_grapes.gif) no-repeat 0px -13px;}
			  td.callout table.callout_2 td {padding: 0px 20px 0px 60px !important; background: url(images/icon_bottle.gif) no-repeat 10px -3px;}
			  td.callout table.callout_3 td {padding: 0px 30px 0px 60px !important; background: url(images/icon_basket.gif) no-repeat 0px -13px; clear: left;}
			  td.callout table.callout_4 td {padding: 0px 20px 0px 60px !important; background: url(images/icon_camera.gif) no-repeat 10px -23px;}
               
              video {width: 416px !important; height: 312px !important;}
              video img {width: 416px !important; height: 312px !important;}

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
				td.promos table.promo_1 {width: 100% !important;}
				td.promos table.promo_1 td {background: url(images/promo_1_small.jpg) no-repeat 0px 40px; padding: 20px 0px 40px 110px;}
				td.promos table.promo_2 {width: 100% !important;}
				td.promos table.promo_2 td {background: url(images/promo_2_small.jpg) no-repeat 0px 20px; padding: 0px 0px 0px 110px; clear: left;}

				td.callout {padding: 20px 30px 0px 30px !important}
				td.callout table {width: 100% !important; margin-bottom: 20px;}
				td.callout table td {padding: 0px 0px 10px 50px !important; background-size: 50px 50px !important; min-height: 60px;}
				td.callout table a {display: inline;}
				td.callout table.callout_1 td {background-position: 0px -6px;}
				td.callout table.callout_2 td {background-position: 4px -2px;}
				td.callout table.callout_3 td {background-position: 0px -7px;}
				td.callout table.callout_4 td {background-position: 4px -17px;}
				td.callout table br.spacer {display: inline;}

                td.footer {padding: 20px 30px !important;}

                video {width: 300px !important; height: 255px !important;}    /*add video rules*/
                video img {width: 300px !important; height: 255px !important;}    /*add video rules*/
			} 
		</style>
	</head>	
```