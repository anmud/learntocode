# Refactoring Challenge

We have a really long code and need to refactor it 

```js
var html = '';
var red;
var green;
var blue;
var rgbColor;

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

red = Math.floor(Math.random() * 256 );
green = Math.floor(Math.random() * 256 );
blue = Math.floor(Math.random() * 256 );
rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')';
html += '<div style="background-color:' + rgbColor + '"></div>';

document.write(html);
```

###  Solution 1

```js
var html = '';
var red;
var green;
var blue;
var rgbColor;
var codeRun = 1; 

function getRandomColor( ){
return Math.floor(Math.random() * 256 );
}

for( codeRun = 1; codeRun <= 10; codeRun ++ ){
 red = getRandomColor();
 green = getRandomColor();
 blue = getRandomColor();
 rgbColor = 'rgb(' + red + ',' + green + ',' + blue + ')'; 
 html += '<div style="background-color:' + rgbColor + '"></div>';
}

document.write(html);
```
### Solution 2

```js
var html = '';

var rgbColor;
var codeRun = 1; 

function getRandomColor( ){
return Math.floor(Math.random() * 256 );
}

function randomColor (){
  var color = 'rgb(';
  color += getRandomColor() + ',';
  color += getRandomColor() + ',';
  color += getRandomColor() + ')'; 
  return color
}

function print(message){
  document.write(message);
}

for( codeRun = 1; codeRun <= 10; codeRun ++ ){
  rgbColor = randomColor();
 html += '<div style="background-color:' + rgbColor + '"></div>';
}

print(html);
```


