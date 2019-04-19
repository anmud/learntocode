# Map & Filter examples

## Why `map`, `filter`?

One of the key foundations of `functional programming` is its use of lists and list operations. In `Javascript` we have `map`, `filter` and `reduce`, all `functions` that given an initial list (array of things), transform it into something else, while **keeping that same original list intact**.

## How to use `Map()`?

```js
const myArray = [1,2,3,4]

const myArrayTimesTwo = myArray.map((value, index, array) => {
    return value * 2
})

console.log(myArray) // [1,2,3,4]
console.log(myArrayTimesTwo) // [2,4,6,8]
```
Here `map` recieves a `callback` as an `argument`. This `callback` itself then get the `current value` of the iterated element, `index` of the iterated element, and  the `original array` from which `map` was called. 

### Examples: 

1. Simple transformation of `array of objects` into an `array of strings`

```js
const songs = [
  {id: 1, name: "Curl of the Burl", artist: "Mastodon"},
  {id: 2, name: "Oblivion", artist: "Mastodon"},
  {id: 3, name: "Flying Whales", artist: "Gojira"},
  {id: 4, name: "L'Enfant Sauvage", artist: "Gojira"}
]

const allSongNames = songs.map(song => song.name)

console.log(allSongNames) // ["Curl of the Burl", "Oblivion", "Flying Whales", "L'Enfant Sauvage"]
```

2. Transforming the given array and adding and removing properties from each object

```js
const songs = [
  {id: 1, name: "Curl of the Burl", artist: "Mastodon"},
  {id: 2, name: "Oblivion", artist: "Mastodon"},
  {id: 3, name: "Flying Whales", artist: "Gojira"},
  {id: 4, name: "L'Enfant Sauvage", artist: "Gojira"}
]

const mapped = songs.map(song => {
  //first we remove the artist property
  const {artist, ...rest } = song
  //return a new object without artist property and with two new properties being added
  return {
    ...rest,
    scrobbleCount: 0,
    spotifyUrl: "let's just imagine these properties make sense for now",
  }
})

console.log(mapped)
//result : 
// 0: {id: 1, name: "Curl of the Burl", scrobbleCount: 0, spotifyUrl: "let's just imagine these properties make sense for now"}
// 1: {id: 2, name: "Oblivion", scrobbleCount: 0, spotifyUrl: "let's just imagine these properties make sense for now"}
// 2: {id: 3, name: "Flying Whales", scrobbleCount: 0, spotifyUrl: "let's just imagine these properties make sense for now"}
// 3: {id: 4, name: "L'Enfant Sauvage", scrobbleCount: 0, spotifyUrl: "let's just imagine these properties make sense for now"}
```

## How to use `Filter()` ? 

`Filter` receives the same `arguments` as `map`, and works very similarly. The only difference is that the `callback` needs to return either `true` or `false`. If it returns `true` then the `array` keeps that `element` and if it returns `false` the `element` is filtered out.

```js
const myArray = [1,2,3,4]

const myEvenArray = myArray.filter((value, index,array) => {
    return value % 2 === 0 
})

console.log(myArray) // [1,2,3,4]
console.log(myEvenArray) // [2,4]
```

### Examples

1. Filter the even numbers

```js

const numbers = [1,2,3,4,5,6,7,8,9,10]

const evenNumbers = numbers.filter(number => number % 2 ===0)

console.log(evenNumbers) // [2,4,6,8,10]
```

2. Do a simle `string` search

```js
const strings = ['hello', 'Matt', 'Mastodon', 'Cat', 'Dog']

const filtered = strings.filter(string => string.includes('at'))


console.log(filtered) // ['Matt', 'Cat']
```

3. Filtering `array` of `objects`

3.1 

```js
const songs = [
  {id: 1, name: "Curl of the Burl", artist: "Mastodon"},
  {id: 2, name: "Oblivion", artist: "Mastodon"},
  {id: 3, name: "Flying Whales", artist: "Gojira"},
  {id: 4, name: "L'Enfant Sauvage", artist: "Gojira"}
]

const mastodonSongs = songs.filter(song => {
return song.artist.toLowerCase() === 'mastodon'
})

console.log(mastodonSongs)
// 0: {id: 1, name: "Curl of the Burl", artist: "Mastodon"}
// 1: {id: 2, name: "Oblivion", artist: "Mastodon"}
```

3.2 

```js
const songs = [
  {id: 1, name: "Curl of the Burl", artist: "Mastodon"},
  {id: 2, name: "Oblivion", artist: "Mastodon"},
  {id: 3, name: "Flying Whales", artist: "Gojira"},
  {id: 4, name: "L'Enfant Sauvage", artist: "Gojira"}
]

const mastodonSongs = songs.filter(song => {
const {artist} = song // use destructuring here 
return artist.toLowerCase() === 'mastodon'
})

console.log(mastodonSongs)
// 0: {id: 1, name: "Curl of the Burl", artist: "Mastodon"}
// 1: {id: 2, name: "Oblivion", artist: "Mastodon"}
```

3.3 

```js
const songs = [
  {id: 1, name: "Curl of the Burl", artist: "Mastodon"},
  {id: 2, name: "Oblivion", artist: "Mastodon"},
  {id: 3, name: "Flying Whales", artist: "Gojira"},
  {id: 4, name: "L'Enfant Sauvage", artist: "Gojira"}
]

// we can destructure song object even in the parameters

const mastodonSongs = songs.filter(({artist})) => artist.toLowerCase() === 'mastodon')

console.log(mastodonSongs)
// 0: {id: 1, name: "Curl of the Burl", artist: "Mastodon"}
// 1: {id: 2, name: "Oblivion", artist: "Mastodon"}
```
## Why use `map`, `filter` and `reduce`?

1. You work directly with the `current value` instead of accessing it through an `index` (i.e array[i]);
2. Avoid mutation of the `original array`, therefore, minimizing `side-effects`;
3. No need to manage a `for loop`;
4. No more creating `empty arrays` and push stuff into them;
5. REMEMBER THE `RETURN STATEMENT` IN THE `CALLBACK`;
6. `Map`, `Filter` and `Reduce` are chainable and, together, you hold an unlimited amount of mystical power!