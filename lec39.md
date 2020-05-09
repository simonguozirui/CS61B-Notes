# Lec 39 Data Compression

### Garbage Collection Continued

Object has different types. Need to search to find object type in a free list.

* Sequential fits (link blocks by FIFO LIFO or address)
* Segregated fits (for different chunk sizes)
* Buddy system (possible to find free chunk by looking at neighbor's chunk)
* Aggregating chunks together

**Garbage Collection**: reuse memory for inaccessible objects

Tunable when we clean it.

1. Reference counter

Reference counter records how many pointers are pointed to the anonymous objects

Release an object when counter = 0.

Used in UNIX file system.

Extra operations and storage, circularity in the structure (doubly linked list, circular list), piece of this structure never goes away.

2. Mark and Sweep

Graph traversal marks everything reachable from roots (local and static variable)

Sweep through memories, find all objects that aren't marked and add them to free list.

Nothing is moved around. Pointers are the same. Amount of work depends on graph traversal (theta(#edges) or linear to size of data) and then how long it takes to sweep through memory (linear to total amount of memory).

3. Copying garbage collection

Copy the objects that are pointed to a new area of memory, leave behind forwarding pointers.

Also copy any pointed pointers objects in to to-space from from-space.

You can swap to-space with from-space and ignore everything in the old to-space. This operation is independent to size of the space.

**Most objects die young**

Generational garbage collection. Avoid copying and copying over.

Garbage collect the new stuff, and don't change the old things.

Make garbage collection quick and real time.



Situations in distributed and parallel garbage collection.

Real-time collection, does not delay execution of program in certain time tolerance.



### Data Compression

Git creates a lot of objects, but you can pack and compress blobs. Take advantage of their similarity.

**Delta compression**

When you have versions, you save distances so you can reconstruct them.

**Unix Compression**

Compression `gzip -k [file] #GNU zip`, `bzip2 -k [file]`

Uncompressing `gunzip` (lossless if we can get back all information)

Compress and compressed file might even be larger.

**Compression algorithm**: stream of symbols --> another smaller stream

Replace 8-bit ASCII bit sequences for digits with 4 bit



Morse code: 3 symbols. You need pre-fix to know if you are getting the signal or the whole signal.

**Pre-fix code** No codeword is prefix of another.

No bit string is a bit string of another.

Encode with HashMap and decode with a Trie



**Create codewords as we go!**

<u>Shannon-Fano Coding</u>

Count frequencies of all characters  in text to be compressed.

Break characters into two groups based on frequencies

Split things as even as we can, repeat until all groups of size 1



<u>Huffman coding</u>

Takes full advantage of frequency

Combine codes, creates a tree. More efficient.



<u>LZW Coding</u>

Codeword that can code multiple symbol

Create new code words as go along, corresponding to substring

Add the code word plus the next character as new entry in codename table.

When you decompress, you can create the table as you go along. No need to have the table beforehand.