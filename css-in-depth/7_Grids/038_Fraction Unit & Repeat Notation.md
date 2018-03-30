# Fraction Unit & Repeat Notation

**fr**
Fraction Unit
describes a fraction of the available space. extra space within the height or the width, that can be divided equally, based on how much space is available. 

**repeat()**
repeat notation: 
repeat(# of repeats, length)

## Values

* **length or persentage** - % are relative to the inline size of the grid container in column grid tracks, and the block size of the grid container in row grid tracks. If size of container depends on the size of its tracks, the % is treated as auto.
* **flex:fr** - positive fr vallue spesifying the track's flex factor. Each fr'ed track takes a share of the remaining space in proportion to its flex factor. 
* **max-content** - equal to the largest of the max contents in the grid track 
* **min-content** - equal to the largest of the min contents in the grid track 
* **minmax (min, max)** - a size between min and less. If max < min then max is ignored, and minmax (min, max) is treated as min. 
* **auto** - as a maximum, identical to max-content. As a minimum, represents the largest minimum size (as specified by min-width/min-height) of the grid items occupying the grid track. 
* **fit-content (lengh or percent)** - represents the formula min(max-content, max(auto,argument)), which is calculated similar to auto (i.e minmax(auto, max-content)), except that the track size is clamped at argument if it is greater than the auto minimum. 