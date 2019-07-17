# Welcome!

This playground is my second one about the BrainFuck language. See the [Getting started with BrainFuck](https://tech.io/playgrounds/50426/getting-started-with-brainfuck/welcome) playground if you didn't already !

While the first playground aimed to talk about basic BF algorithms, this ones will introduce one of the most used data structure : arrays.

In case you're still wondering : yes, the cover image is, again, the source code of a BF interpreter, written in BF ^^. This will be part of the 3rd playground :-)

# Let's start

Let's first define how we will structure our array in memory. For this first draft, we will define some hypothesis:
* An array contains values (0 or more)
* It is represented in memory by a succession of cells, each one being a value
* The array is *delimited* in memory using _0_ values (the array has to be somehow delimited)
* Due to the delimiters definition above, an array cannot contains a 0 value
  * But and array can be empty, of course
* Memory will look like 0, value1, value2, value3, ..., valueN, 0 with all valueX greater than 0

*Note:* at the end of this playground, we will see how we can have null values in arrays, using a different data structure. But it is really important to understand the basic algorithms first !

Now, let's implement basic operations on arrays
