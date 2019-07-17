# Deal with null values

As explained, it is not possible to deal with null values in our arrays, and that may be an issue in most of the case.

Having explained all the mechanisms of arrays (get, reverse, length, move, ...), we can however adapt them to a new data structure: 2-cells arrays.

In this implementation, an N-value-long array is not only composed by N cells + 2 delimiters. It's still N+2 "blocks", but each block will be composed by 2 cells
* isValue flag: 0 if it's an array delimiter, or 1 if it's an array cell
* value cell: does not matter if isValue is 0, or cell value (including null value) if isValue is 1

In other words, the "not-null-required" hypothesis is transposed on the first part of the cells, and the value is now free to be null.

Note that this implies twice more memory for arrays, so based on the use case, we should decide whether null values are admitted or not.

All the algorithms can be transposed here, we will just learn how it works from a test program

# Test program

This program reads digits from the input, convert them into values (subtract 48) into an array, then print them back as digit (add 48 and print)

Note : as coded here, we can leverage the extra cell for faster execution. For example, it would not have been possible to iterate and add 48 at the same time in regular 1-cell arrays.

```
>>>>,                  create empty delimiter block then read value
[                      while a digit is read
  <++++++++[->------<] subtract 48 (leverage the isValue flag cell for this)
  +                    set isValue flag to 1
  >>>,                 read next value
]                      loop
<<<[<<]>>              go to first cell (note the doubled moves because of "2 cells a block" design)
[
  +++++++[->++++++<]   add 48 to each digit (use isValue flag again)
  +>.                  set back isValue flag and print digit
>]                     go to next cell (be careful to point at the next isValue flag
```

As 0 is a supported digit, we can see that null values are correctly handled by this code.
