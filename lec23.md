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

move bottommost, rightmost node to to, then re-heapify down as needed (swap offending node with larger child) to re-establish heap property. We do this to guarantee the shape of the heap.

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

