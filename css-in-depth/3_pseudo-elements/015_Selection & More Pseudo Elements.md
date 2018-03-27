# Selection Disable

Sometimes we want to disable selection. But you should almost never use this. 

```css
.thisSlide.foo {
  -webkit-tap-highlight-color: #bada55;
  -webkit-user-select: none;
  -webkit-touch-callout: none;
}
```

### IE10 Specific Elements

```
::-ms-browse

::-ms-value

::-ms-check

::-ms-clear

::-ms-expand

::-ms-fill

::-ms-fill-lower

::-ms-fill-upper

::-ms-reveal

::-ms-thumb

::-ms-ticks-after

::-ms-ticks-before

::-ms-tooltip

::-ms-track
```
### Shadow DOM

Many, many more pseudo-elements with prefixes currently treated as a shadow DOM

```
::-webkit-progress-bar

::-webkit-progress-value

::-webkit-meter-even-less-good-value

::-webkit-inner-spin-button /outer-spin-button

::-webkit-validation-bubble / arrow-clipper /arrow /message
```

