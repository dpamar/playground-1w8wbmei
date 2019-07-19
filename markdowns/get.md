# Get item by index

Well, wait, this is the most important operation ! Why is it presented after useless things like moves, shifts, etc... ?

The reason is, there is no direct memory access in BF. We cannot say "I want value of memory cell X" and therefore accessing Array[X], generally done in any language by getting memory value of _memory address of Array + X * size of Array items_, cannot be done this way in BF.

Instead, we will use moves, shifts, etc... to get item #i from an array. The process will be:
* have in memory _0, 0, Array, 0, target index, 0_
* during the process, it will be _0, ArrayA, 0, ArrayB, 0, target index_ with Array=ArrayA + ArrayB
* while target index is not null
  * go to the first element of ArrayB
  * move it to the left (last element of array A)
  * then decrease target Index
  * Memory will by
    * before first pass _0, ArrayA, 0, X, ArrayB, 0, target index_
    * after moving X _0, ArrayA, X, 0, ArrayB, 0, target index_
    * after index decrease _0, ArrayA, X, 0, ArrayB, 0, target index-1_
* get first element of ArrayB
  * move it to the end of ArrayA first (otherwise we cannot move along ArrayB if this value is going to be null)
  * move it after ArrayB, twice
  * move back one of the copy at the end of ArrayA
  * Memory will by
    * before first pass _0, ArrayA, 0, target, ArrayB, 0, 0, 0_
    * after first move pass _0, ArrayA, target, 0, ArrayB, 0, 0, 0_
    * after second move pass _0, ArrayA, 0, 0, ArrayB, 0, target, target_
    * after last move pass _0, ArrayA, target, 0, ArrayB, 0, target, 0_
* and finally, move ArrayA back to its initial location


# Let's start

* Memory: 0, 0, Array, 0, target index, 0
* Cursor: on target index
* Input: any

# Process

* _invariant: memory is 0, ArrayA, 0, ArrayB, 0, index, 0 with Array = ArrayA + ArrayB and target is ArrayB[index]_
* while index is not null
  * go to ArrayB first element
  * move to the left
  * go back to target index and decrease
* loop
* _index = 0: target is ArrayB[0]_
* go to ArrayB first element
* move to the left
* copy twice after ArrayB
* go to second copy
* move it back after ArrayA
* move ArrayA back to its initial location

# Code
```
[                               while index is not null
  <<[<]>                        go to ArrayB first element
  [-<+>]                        move to the left
  >[>]>-                        go back to target index and decrease
]                               loop
<<[<]>                          go to ArrayB first element
[-<+>]                          move to the left
<[->>[>]>+>+<<<[<]<]            copy twice after ArrayB
>>[>]>>[-<<<[<]<+>>[>]>>]       go to second copy and move it back after ArrayA
<<<[<]<[[->+<]<]>               move ArrayA back to its initial location
>[>]>                           go to the result value
```

# Minified version
```
[<<[<]>[-<+>]>[>]>-]<<[<]>[-<+>]<[->>[>]>+>+<<<[<]<]>>[>]>>[-<<<[<]<+>>[>]>>]<<<[<]<[[->+<]<]>>[>]>
```

# Final state

* Memory: 0, 0, Array, 0, Array[target index], 0
* Cursor: on result
* Input: unchanged
* Output: unchanged

# Test program

This program first reads *exactly* 10 chars from input, then any number of digits.

For each digit, it prints the Array[digit] value

```
>>,>,>,>,>,>,>,>,>,>,>>,              read exactly 10 chars then first index to process
[                                     while there is an index to process
  <++++++++[->------<]>               convert decimal digit into a value (subtract 48)
  [<<[<]>[-<+>]>[>]>-]<<[<]>[-<+>]<   get Nth item
  [->>[>]>+>+<<<[<]<]>>[>]>>[-<<<[<    ** part 2 **
  ]<+>>[>]>>]<<<[<]<[[->+<]<]>>[>]>    ** part 3 **
.,]                                   print result; read next index and loop
```

Example with an input abcfiknru!17046382599999 : ouput is brainfuck!!!!!

