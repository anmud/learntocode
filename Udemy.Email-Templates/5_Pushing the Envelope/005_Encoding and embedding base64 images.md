# Encoding and embedding base64 images

The other way to specify graphics and embed it into html is to URI encode our `images` (use `ascii code`). 

![ascii-code](..ascii-code.png)

This is a pattern of text which is encoded in the `base64` format which can then be turned back into a `graphic` in a page. 

![ascii-code-2](..ascii-code-2.png)

Typically with graphics we specify this with `html tag`, `image tag` with the source equalling the actual file name. To make use of `base64` code we will still use an `image tag`, but the source here is gonna equal `data:` that we ganna give it a name, specify `base64` and then add all of the code that's representing our graphic. 

![ascii-code-3](..ascii-code-3.png)

To create `base64` images we can use online tools, or some text editors might have build-in plugins. We can copy this code and paste it into out html `img` tag. 

![logo-base64](../logo-base64.png)

Keep in mind is that representing binary data as `ascii` is goint to be a little bit larger in file size; the up side is - there is no second call to the server. 