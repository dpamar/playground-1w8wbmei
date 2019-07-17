# Go to the beginning / end of the array

With arrays stored in memory, we should be able to access memory either _before_ or _after_ the array location.

We know that our cells are not null, and thanks to this we can use the magic operation `[>]` (or `[<]`) : move to the right / left until you find an empty cell.

# Let's start

* Memory: 0, Array, 0
* Cursor: on first 0 cell
* Input: any

# Process

* move to the right (into the array)
* while current cell is not null
  * move to the cell on the right
* loop

# Code
```
>     move to the right (into the array)
[     while current cell is not null
  >   move to the cell on the right
]     loop
```

Minified version
```
>[>]
```

# Final state

* Memory: 0, Array, 0
* Cursor: on second 0 cell 
* Input: unchanged
* Output: unchanged


# Variants

To go back to the first 0 cell
```
<[<]
```

To reach array first cell while in the array
```
[<]>
```

To reach array last cell while in the array
```
[>]<
```

# Test program

This program reads multiple chars from input (at least 3 chars are expected).

The N chars are split in memory into 
* first char
* N-2 middle chars
* last char

Then, it goes back to the first char and print it; then on the last one and print it; and finally prints the array from 2nd to N-1th items.

```
,          read first char
>>,[>,]    have a 0 separator for the array then read all the other chars
<[->+<]    move the last input char to have a 0 separator
           Memory looks like A 0 B C D E F G H I J K L M N O P Q R S T U V W X Y 0 Z
           if input was the entire alphabet; and the cursor is just before Z
<[<]<.     Go to first char and print
>>[>]>.    Go to last char and print
<<[<]>     Go to array first value
[.>]       Iterate on the array : print and move
```



