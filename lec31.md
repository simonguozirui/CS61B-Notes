# Lec 31 Balanced Search Structures (II)

Red-black tree mimics 2-4 Tee, both balanced; redness and badness replaces nodes with cluster of keys

Rotation: make one side shorter at the expense of the other

Changes the shape of the tree

Rotation Recoloring: maintain 2-4 tree property while preserving red-black tree property.

**Red nodes only suppose to have black nodes as children!**



Red nodes are constitutions of a 2-4 node in effect.

`colorFlip`: one black node, 2 red children --> one red node, 2 black children

Effectively splitting a big 2-4 tree node, original black joins parent node

**Red-Black Tree mapping to BTree**: 

Each 2-4 Tree node is represented by a cluster of red and black nodes.

With the black nodes at the top. All the red nodes are the siblings in the BTree of the parent (in red-black tree)

In a red-black tree, black on top, a single node containing below. Red on top, parent and children are separate for below.



Always insert a red node except for root to avoid changing balance of black nodes



### Fix Ups 

Looking at LLRB and (2,3) trees

1. Convert right-leaning trees to left-leaning: via rotations (`rotateLeft`)
2. Rotate linked red nodes into 4-node temporarily: via rotations (`rotateRight`)
3. Break up 4-nodes into 3 nodes or 2-nodes: via `colorFlip`, color representation of BTree node
4. If we are done at the root, if it is a red node, turn it into black to satisfy to the LLRB invariants.

 

We do fix up on the way back up during the recursion.



It is perfectly fine to have all black nodes! All we care is the path length and black nodes to be balanced.

Red-red indicates a node is too big or ill-formed



### The Trie

What are the cost of comparisons? Not necessarily constant. For example, string with different length.

theta(M) comparisons really mean theta(ML) operations where L is max key length

Can we turn this into O(L) for searching for a string of length L? No matter how big how much data the tree has.

**Does not depend on size of tree, but on the size of things we look for!**

### Multi-Way Decision Tree instead of Binary

Each internal node corresponds to a possible prefix for string. 

You can find strings that contains the prefix in addition to finding the exact string.

pre-order traversal we get all the keys in-order; sorted set

Similar idea to radix sort. Searching algorithm corresponds to sorting algorithm.



Array Access is constant time we can say. 

Each node is an array of children, using letters, 26 pointers

Thus O(L) performance seems independent of N. There is a weak dependence (the more keys the further down you have to go down) not a big effect





We can also do a Linked List of linked children, slower to access.

Arrays for first levels, linked list for the end.



**Scrunching**

These arrays have a lot null children, we put them on top of each other.

Overlay them, you have to shift them sometimes, expand the combined array.

We keep track of the original index of each element in their original index on top of the position of the combined array

See slides for info. We keep track of where each array starts counting too (the shifted position)

If the value is null, it is null. If the value is null but indexes don't match, then I know the actual value is null.

Used in constant table to save space.

Insertion could cause issue, complicated.

Number of children goes down going down the array, might as well use Linked List.



### Probabilistic Balancing: Skip Lists

Have two sentinel nodes, don't contain valid info, just makes life easier.

Search along different levels

Sort of binary search but not quite.

Every time we insert an element in the list, we insert a heaps of pointers with it with random number of them

#have 1 pointer = 2* #have 2 pointers = 4* #have 3 pointers

A kind of multi-way search tree with multiple randomly-chosen keys

If chosen randomly, at high probability, our search tree will be log N



### Summary

**How to get lgN performance from search trees?**

* BTree & red-black
  * guaranteed lgN worst case for searches, insertions, and deletions.
  * BTree has big nodes, good for external storage.
* Tries
  * theta(B) length of key, but hard to keep space efficiently
    * could use scrunching for sparse array to be take less space
* Skip lists
  * Theta(lgN) is very fast, probabilistic algorithm
  * We met similar idea in quicksort where if we randomly permute data before sorting, we highly likely get NlgN time instead of N^2.



Java implementation, have some but not all concepts comparing to other languages



### Data Structure that Implement Abstractions, as well as corresponding Java classes

Multiset `Collection`

* List: arrays, linked lists, circular buffers; `ArrayList`, `LinkedList`, `Stack`, `ArrayBlockingQueue`, `ArrayDeque`
* Set
  * OrderedSet
    * Priority Queue: heaps, `PriorityQueue`
    * Sorted Set: binary search trees, red-black trees, B-trees, sorted arrays or linked lists, `TreeSet`
  * Unordered Set: hash table, `HashSet`

Map

* Unordered Map: hash table, `HasMap`
* Ordered Map: red-black trees, B-trees, sorted arrays or linked lists, `TreeMap`



