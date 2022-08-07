# MakeShards: External Sort - Buffered Streams

This small program creates new files that contains all the same words as `unsorted.txt`,
but in the new files they should be sorted alphabetically.

It should be noted that the end goal is to create a new file that contains 
all the same words as `unsorted.txt`, but in the new file they should be sorted alphabetically.

For the purposes of this exercise, we are only sorting 10,000 words in different files
where each files contain at most 100 words (the shard size). 

We pretend that those 10,000 words won't fit in the computer's memory
and to deal with this pretended limitation, 
we use a technique known as [External Sorting](https://en.wikipedia.org/wiki/External_sorting), 
which is a way to sort large amounts of data. At a high level, this involves :

1. *sharding* the large file, which means splitting it up 
    into a bunch of smaller files that can individually fit into memory;
2. *sorting* the shard files; and
3. *merging* the sorted shards into a single large sorted file. 
   The merge can be done in a way that does not require loading all the sorted words into memory at once.

In this exercise, only Steps 1 and 2 are implemented. `List#sort()` is used to do the sorting 
(`Stream#sorted()` could also be used).

The unsorted words from the `input Path` are read, line by line, using a `BufferedReader`. 
The input words are written to the many shard files. 
Each shard file contain at most `SHARD_SIZE` words, in sorted order.
All the words are accounted for in the output shard files; No word is skipped.

Once we are done sorting the words for a shard, we write the sorted shard file to the `outputFolder Path`, 
using a the `getOutputFileName(int)` method to name the individual shard files. 
`BufferedWriter` is used to do the writing.


## Running the code

To compile and run the code, just do:

    javac MakeShards.java
    java MakeShards unsorted.txt shards/


