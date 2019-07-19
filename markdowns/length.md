# Get array lengh

This is one of the most common operations generally performed on arrays : how many items are stored into ? But it's not really straightforward to implement...

We need to count items in an array and store the result after the array itself. It can be done by
* having 2 arrays, the left part for "not-counted-yet" items, and the right part for "already-counted" items
* go to the rightmost part of the 1st array, move it to the leftmost part of the 2nd one and increment counter
* repeat until the 1st array is empty
* and do some cleansing: put the whole array at its original place

# Let's start

* Memory: 0, Array, 0, 0, 0
* Cursor: on 0 cell after the array
* Input: any

# Process

* _invariant: memory is 0, ArrayA, 0, ArrayB, 0, N with N = length(arrayB) and Array = ArrayA + ArrayB_
* while last cell of ArrayA is not null
  * move the the right (first cell of ArrayB)
  * go to the end of ArrayB and increase N by 1
  * go back to the end of ArrayA
* loop
* _memory is 0, 0, Array, 0, length(Array)_

# Code
```
<[         while last cell of ArrayA is not null
  [->+<]   move the the right (first cell of ArrayB)
  >[>]>+   go to the end of ArrayB and increase N by 1
  <<[<]<   go back to the end of ArrayA
]          loop

```

# Minified version
```
<[[->+<]>[>]>+<<[<]<]
```

# Final state

* Memory: 0, 0, Array, 0, length(Array) 
* Cursor: on first 0 cell
* Input: unchanged
* Output: unchanged

# Variant

Cleansing : put back the array at its original location; final memory : 0, Array, 0, 0, length(Array)
```
<[[->+<]>[>]>+<<[<]<]   compute length
>>[[-<+>]>]             move array back
```

# Test program

This program reads up to 9 chars, store them into an array, then print length (limited to 9 because number to decimal string conversion will be needed otherwise)
```
>,[>,]                  read chars
<[[->+<]>[>]>+<<[<]<]   compute length
>>[[-<+>]>]             move array back
++++++++[->++++++<]>.   add 48 to length (48 is '0' ASCII code; it converts an integer into a decimal digit); and print length
```
