# While Loop Challenge

1. Write a `while` loop to build a string of numbers from `0` to `4`, separated by spaces, and store the string in the variable `text`.

```js
let i = 0;
let text;


while( i <= 4 ){
  text += i + ' ';
  i +=1;
}

print(text); // Should print `0 1 2 3 4 `.
```

2. Write a `while` loop to build a string of numbers from `1` to `5`, separated by spaces, and store the string in the variable `text`.

```js
let i = 1;
let text;

while( i <=5 ){
  text += i + ' ';
  i +=1;
}

print(text); // Should print `1 2 3 4 5 `.
```

3. Write a `while` loop to build a string of numbers from `5` to `1`, separated by spaces, and store the string in the variable `text`.

```js
let i;
let text;

i = 5;
while( i >= 1){
  text += i + ' ';
  i -=1;
}

print(text); // Should print `5 4 3 2 1 `.
```
4. Write a `while` loop to build a string of numbers from `5` to `50--by 5's`. The numbers should be separated by spaces, and stored in the variable `text`.

```js
let i;
let text;

i = 5;
while( i <=50){
  text +=i + ' ';
  i +=5;
}
print(text); // Should print `5 10 15 20 25 30 35 40 45 50 `.
```

5. BONUS CHALLENGE: Write a `while` loop that builds a string of random integers between `0` and `9`. Stop building the string when the number `8` comes up. Be sure that `8` does print as the last character. The resulting string  will be a random length.

```js
do{
  i = Math.floor( Math.random() * 9);
  text+= i + ' ';
} while( i !== 8){
}

print(text); // Should print something like `4 7 2 9 8 `, or `9 0 8 ` or `8 `.
```

