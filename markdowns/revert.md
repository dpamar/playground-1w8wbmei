# Revert array

The goal is to reverse an array (i.e. A,B,C,D -> D,C,B,A). More difficult: the goal is to have an in-place implementation.

In place means that we don't need any extra memory to do it, or more precisely that the amount of extra memory needed is constant regarding the array length.

The principle is: our memory looks like 0, Array, 0, 0
* We will have 0, ArrayA, 0, ArrayB, 0 with Array = ArrayA + revert(ArrayB)
* Start with the last (rightmost) cell of ArrayA
* Move it to the last (rightmost) cell of ArrayB
  * This part is tricky : move is done with successive +1/-1 but
    * we cannot go to the 0 delimiter after ArrayB : if we add 1 the first time, then it won't be empty for the second +1/-1 round...
    * therefore, we need to move it to the cell *after* the 0 delimiter
    * And finally, when value has been moved completely, move it to its final position
  * _Memory before first pass: 0, ArrayA, X, 0, ArrayB, 0, 0_
  * _Memory after first pass: 0, ArrayA, 0, 0, ArrayB, 0, X_
  * _Memory after second pass: 0, ArrayA, 0, 0, ArrayB, X, 0_
* Shift ArrayB to the left

# Let's start

* Memory: 0, Array, 0, 0 
* Cursor: on Array last cell
* Input: any

# Process

* _invariant : memory is 0, ArrayA, 0, ArrayB, 0 with Array = ArrayA + revert(ArrayB)_
* while ArrayA last cell is not null
  * Move it after rightmost 0 delimiter of ArrayB
  * then, move copied value after ArrayB
  * shift ArrayB to the left
  * go back to ArrayA last cell
* loop
* _ArrayA is empty, so memory is 0, 0, ArrayB, 0 with Array = revert(ArrayB), so arrayB = revert(Array)_

# Code
```
[                 while ArrayA last cell is not null
                  Move it after rightmost 0 delimiter of ArrayB
  [-              decrase by 1
    >>[>]>+       go to target and increase by one
    <<[<]<        go back to source
  ]               and loop
  >>[>]>[-<+>]    then move copied value after ArrayB
  <[<]>[[-<+>]>]  shift ArrayB to the left
  <<[<]<          go back to ArrayA last cell
]>                loop, and go back to left delimiter of revert(Array)
```

Minified version
```
[[->>[>]>+<<[<]<]>>[>]>[-<+>]<[<]>[[-<+>]>]<<[<]<]>
```

# Final state

* Memory: 0, 0, revert(Array), 0
* Cursor: on left 0 delimiter of the array
* Input: unchanged
* Output: unchanged

# Test program

This program reads as many chars as possible, stores them into an array, reverse the array then print it reversed

```
>,[>,]<                                               read as many chars as possible
[[->>[>]>+<<[<]<]>>[>]>[-<+>]<[<]>[[-<+>]>]<<[<]<]>   revert the array
>[.>]                                                 iterate on the array ; print and move
```
