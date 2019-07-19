# Shift array in memory

The goal of this operation is to move all the memory cells of our array on the left (or right)

To append on the left, we should start on the rightmost cell and move it to the right, then go to the cell on the left and redo the same until we reach the beginning of the array

# Let's start

* Memory: 0, Array, 0
* Cursor: end of the array (on 0)
* Input: any

# Process

* go to array last cell
* while current array cell is not null
  * move it to the right
  * go to left
* loop

# Code

```
<          go to array last cell
[          while current array cell is not null
  [->+<]   move it to the right
  <        go to left
]          loop
```

# Minified version
```
<[[->+<]<]
```

# Final state

* Memory: 0, 0, Array, 0
* Cursor: first 0 cell 
* Input: unchanged
* Output: unchanged

# Variant

To move the entire array on the right (while on first 0 delimiter)
```
>[[-<+>]>]
```

# Test program

This program reads 5 chars. The first 4 ones are put into an array, then the array is shifted to the right and the fifth char is read directly on the new cell. Memory looks like:
* 0 0 0 0 0 0 0 0 then read A
* 0 A 0 0 0 0 0 0 then read B
* 0 A B 0 0 0 0 0 then read C
* 0 A B C 0 0 0 0 then read D
* 0 A B C D 0 0 0 then shift
* 0 0 A B C D 0 0 then read E before A
* 0 E A B C D 0 0
And finally, prints the whole array as it is stored in memory

```
>,>,>,>,    read A B C D
[[->+<]<]>  shift array on the right
,           read E
[.>]        iterate on the array : print and move
```
