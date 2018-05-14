# More Browser APIs

There are many things where waiting would block our `thread` and we use `Browser APIs` for instead
* A timer to finish running
* New information from a server (Ajax)
* Indication that a portion of the page has loaded
* User interaction (clicks, mouseovers, drags)
* Writing/Reading to File system (Node)
* Writing/reading database (Node)

Some of the APIs (built in features in the browser) they actually speak to somewhere else of outside the browser, like a server. They come back with data. 

Some come back with data. The design of the Browser API we are using determines how we access the returned data. 
That we were waiting on to run our deferred functionality. 
```js
function display(data){
console.log(data.post);
}
$.get("http://twitter.com/willsen/tweet/1", display);
console.log(“Me first!”);
```

### XML HTTP Request

**Line-by-line**
1. we declare `display` function
2. we pass to `$` function (jQuery function) a string - `http://twitter.com/willsen/tweet/1`,  and the whole `display` function definition.
Actually, `$` function does nothing in JS land, it speaks to the browser API. We should look in the jQuery documentation to know how this `$.get` works.
3. so, our `$` function speaks to the web browser feature : namely - `XMLHttpRequest`, and takes in reference to our functionality and our URL.
4. In web browser API land we create a `xmlhttprequest`, and assosiated with it our functionality `display`. 
5. it sends the message to twitter (outer API)
6. now `$` function gets done its work 
7. now we get back to global and our code console.logs "Me first!"
8. behind the scenes our `xmlhttprequest` comlete, actually, we've got the data from twitter 
9. now we put our `display` function with assosiated data to the `callback queue`
10. then we check with `event loop` was the `call stack` clear, and ask 'is there something in the callback queue?'
11. then we push our `display` function to the `call stack`, and now its first `parameter` is filled with the data we got. 
12. now we have a new `execution context` with our `display` function, and in the first parameter we have an `object {post: hi}` , namely data we got. 
13. the `function` runs and console.logs `"Hi"`





