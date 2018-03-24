# Selector Structure

In CSS you can target anything and style it the way you  want. Fex. here we style every 3-rd list item, using selectors.

``` 
li: nth-last-of-type(3n){
color:#E2007A
}
``` 

![my image name](./listItemsStyle.png)

Here are the examples of selectors structure:

```
 selectorB{
    property1:value1;
    property2:value2;
}
```


```
selectorB{
    property1:value3;
    property2:value4;
 }
 ```

```
selector: pseudo-class::pseudo-element{
    -vendor-property: value;  
}
```

```
selector[attribute],
selector ~ relation{
    property: -vendor-value;
    -vendor-property: -vendor-value;
    -vendor-property: weirdsyntax;
}
```

Some of this will be prefixed. Generally you don’t use prefix properties. But remove the most border radius and remove a webkit, and your gradient from your code. The reason a lot of CSS properties stay prefixed used to be because of the performance. 
If you use webkit border radius or webkit border gradient the only device that needs this is an old android device. 

# Preprocessors



