# Lec 23 Priority Queues, Range Queries

Theme: searching throughs collection of data

### Priority Queues, Heaps

priority queue is the abstract idea, heap is an implementation of it

Priority queue, operation: `add`, `find largest`, `remove largest`

Long stream of actions, schedule them as they come in.

Execute the largest, remove it.
Or use it for sorting, repeatedly remove the largest, and then build up the collection with the removed largest. You will sorted the elements.

Go-to-implementation is the heap.

There are multiple implementations in Java that achieve the same goal, for example: `TreeSet`



### Heaps

Typical binary tree

Heap property: labels of both children of each node are less node's label. (A **max** heap, there is also min heap).

Node at top has largest label.

Looser than binary search property, children could occur in any order. For a max heap, always valid to put the smallest nodes anywhere at the bottom of the tree.

Thus, quite easy to maintain the ideal of a bushy tree, whose height is proportional to the logarithmic of the amount of data held. All operations operate in logarithmic of total amount data, which is fast.

Heap is nearly-complete. All but last row have as many keys/children as possible.

Any insertion of new value or deletion of largest value always takes logN in worst case. 



Insert from left to right, fill up current level before moving to next level



Swap is safe operation due to the existing heap property before insertion. It re-establishes the heap property.

Time is logarithmic to the number of nodes (as worst case go to the top and we stop at the root)



**Finding** top node, very easy

**Removing** the largest node    

move bottommost, rightmost node to top, then re-heapify down as needed (swap offending node with larger child) to re-establish heap property. We do this to guarantee the shape of the heap.

Each stage look at two nodes, two operations + swap each level, total amount of time required is proportional to log N



For a sequence of operation, is number of operation * logN, things tend to be dominated by the removal and reheapifying operation.



### Heaps in Arrays

How to take advantage of the fact that heap is nearly complete.

Instead of objects and pointers, save the label values in level order in an array.

Instead of pointer, array indices. Instead of objects, elements of an array. Change of representation.

Start indexing at 1.

Find your children:

Children of node at index #K are in 2K and 2K + 1 if numbering from 1, or 2K+1 and 2K+2 if from 0.

Find your parent: integer division by 2.

We can tell when we have a null child (go over array size)



Easy to find the node that you need to move up to the top during removal largest entry, just look at end of the array .



How to speed up the initial formation of the heap? Will come back when talking about a sorting technique called Heap Sort.



### Ranges

Back to BST.

Want to find all values in a particular range.

Similar to the BST search algorithm, but use multiple ifs to leave possibilities to explore.

Doing 2 recursive calls, that seems exponential explosion. Worst case all the nodes of tree.

But not every time we call 2 recursive calls exponentially.

We look into spines, which at most height of the tree h.

Everything within the bound of this spine, on the left and right, is fair game.

The total amount of time to traverse this tree is O(h+M) where h is height of the tree, and M is number of data items that turn out to be in the range. This is true as you do a certain amount of work every time you find a data item.

Height of the tree + number of items that we need to add to the range, this is time of this range query.

M depends on L and U. M can be very small if you have a narrow range.

Can't do any better than M because I need to visit all the nodes in the range!



Good engineering: don't repeat work if someone did it already.

Java gives us

* `SortedSet` supports range queries, return views of set (type `SortedSet`)
  * `S.headSet(U)` subset of S that is < U
  * `S.tailSet(L)` subset of S that is >= L
  * `S.subSet(L,U)`subset of S that is >= L, < U
  * Any modification you make to them get made in the original set S, as these are views.
* You can iterate through a view to process a range. 
  * `for (String item : x.subSet("B", "G"))`


If we add something to the set, the view gets updated.

If we add something to the view, the set gets updated.



View is distinct from slice (which is a new copy of the data).

Views are second objects that shares information with objects that it came from.



How to create a copy of the subset that does not affect the original set?

`new TreeSet(S.subSet(L,U))` get a copy due to Java collection classes constructor that takes a collection as the argument and copy of the data of collection.



**TreeSet**

* Concrete implementation of `sortedSet`in Java.
* TreeSet<T> requires either that T be Comparator or that you provide a Comparator, which is a type of a function object `Comparator<T>.compare(T left, T right);`
* `SortedSet<String> x = new TreeSet<String(Collections.reverseOrder())>; `create a TreeSet according to this ordering.

Reverse order implementation applies `compareTo` operation on two elements **in reverse**. `y.compareTo(x)` instead of `x.compareTo(y)`.

newer Java feature, one line lambda expression to create Comparator<T>.

```java
static <T extends Comparable<T>> Comparator<T> reverseOrder() {
    return (x,y) -> y.compareTo(x);
}
```



### Heapify

Sure! Let's go through an example: 

```
           A               // level 0
        /      \
       B        C          // level 1
     /   \    /   \
   D       E F      G      // level 2
  / \     /| |\    /  \
 H  I    J K L M   N   O   // level 3
```

Let's just use this example tree where we refer to each node by its letter. It has 4 levels and 15 nodes. If we want to heapify, we would bubble down everything in the lower levels and then the upper levels, i.e. level 3 nodes (H-O) are bubbled down first, then level 2 (D-G), then level 1 (B-C), and then level 0 (A). We start at N/2 because we're assuming that that's the index of the first node on the bottom level (H) which is what we actually want to start at. If we bubble down in this level order, we can ensure the final heap maintains the heap property. When we bubble down, the amount of operations it should take is proportional to how far from the bottom of the tree each node is. Nodes in level 3 can swap down at most 0 times. Nodes in level 2 swap down at most 1 time. Nodes in level 1 swap down at most 2 times. Nodes in level 0 swap down at most 3 times. Let's assume worst case, so each node ends up swapping down as much as it can. Then the total number of swap operations would be

 

```
 (# nodes in level 3) * 0 + (# nodes in level 2) * 1 + (# nodes in level 1) * 2 + (# nodes in level 0) * 3 
= 8 * 0 + 4 * 1 + 2 * 2 + 1 * 3 
= 11
```

 

In other words, half the nodes don't even swap down at all since they're at the bottom already, half of the remaining swap down at most once, half of the remaining swap down at most twice, and so on. This happens to follow a pattern where if you sum up the number of swaps, the maximum number of swaps is O(N).

 

For a heap with height h (the tree above has height 4), the summation would be

 

```
(# nodes in level h-1) * 0 + (# nodes in level h-2) * 1 + (@ nodes in level h-3) * 2 + ... + (# nodes in level 0) * (h-1) 
= N/2 * 0 + N/4 * 1 + N/8 * 2 + ... + 1 * h-1
= some number that is O(N)
```

 

\----

Now the reason why in heapify we start at the bottom levels and then bubble down (heapify down) versus starting at the top levels and bubbling up (heapify up) is that the former is more time efficient. To hint at why that would be: There are about N/2 nodes in the bottom level of the heap. If we have to bubble all of them down (heapify down), that would be at most 0 swaps per node. If we had to bubble them up (heapify up), that would be at most h -1 swaps per node. There is only 1 node at the very top of the heap. If we had to bubble it down (heapify down), it would take at most h-1 swaps. If we had to bubble it up (heapify up), it would take at most 0 swaps. Knowing that, which method seems more efficient? The method where you make the 1 root node swap down at most h-1 times (heapify down), or the method where you make N/2 nodes swap up at most h-1 times (heapify up)?