# Gatsby-image fluid Details

Well, we use the `image` of the one size, but the users visit our site let's say from the phone and then the massive `image` we have doesn't suit in this case.  We could do our `image optimisations` manually, but where `gatsby-image` really helps - is that `gatsby` behind the sceneces creates for us multiple images with different sizes - it gives basically a `browser` a choise which size of the picture to use with any kind of devices, depending on which device a user is using. 

There is though a common misconseption concerning `max width`. If we are using `max width` argument for the `fluid image` in fact that makes sure that the image never gets bigger. 
> **BUT** what we need to remember here is that `fluid image` **will always be the size of the `parent`**. If our `image` is inside some parent `div` it will have the size of this parent `div`, even if the `fluid image` has the `max width` less than the parent `div`/container. 

What is in fact happenning? The `max width` argument by default is `800px`. Actually by using `max width` argument we are controlling which sizes of the image will be  generated. Let's imagine we know our parent `div` will be 600px, what we can say - ok my `max width` will be 600px,  `graphql` will generate the `sizes` that are **closer** to our `max width`. But it will not controll the actuall `width` of the `image`, cos the `width` of the `image` will always be controlled be the `parent container`. 



