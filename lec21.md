# Lec 21 Tree searching

Using several depth-first traversal, get the breadth-first order.

Even you seem to do more work, if your tree is bushy, the amount of work you do is just constant more than normal BFS.

Fun Fact about trees, number of nodes at given level, is the same as total number of nodes above it - 1.



### Tree Iterators

`hasNext()`, `next()`

Give you the next thing in the traversal of the tree

Easily use a for loop. 

However, this is not intuitive compared to recursive version. It is breaking down iterative DFT code.

What `next` does is to pop the node from the stack, add its children to the stack (in right to left order for adding to the stack, so the left one will be first to pop off).



We can iterate the tree iterator if the Tree has a method `iterator` that returns an iterator

`for (String label : aTree) System.out.print(label + " ");`



**Tree Representation**

Mostly can be represented in arrays and pointers

1. Embedded child pointers + optional parent pointers
2. Array of child pointers + optional parent pointers
3. Child/sibling pointers
4. Breadth-first array (complete trees, ex. heap): Use array indices to indicate their position (parent /child relationship), for a tree that every node with same number of children.



Trees represent hierarchy of data.

What does hierarchy mean? Searching, hierarchy --> Divide and conquer

Break problem down recursively into small pieces to attack

How to find something in a collection of data?

A node can either contains data, and <u>some information we use to decide which child might contain the output.</u>

Smaller parcels than total amount of data



Decision data --> no, or yes (which one go down) or decision data --> low, mid, high (which are we suppose to pick to go down?)



If we divide information evenly, structure of tree: height is **logarithmic** of the size of the data

That is a very fast algorithm.



### Binary Search Tree

Tree node contains keys, possibly other data. For searching, we are interested in the keys only.

We don't allow duplicate keys in this semester. We are dealing with a set for now.

**Binary Search Property**:

* All nodes in left subtree of node have smaller keys

* All nodes in right subtree of node have larger keys



The number looked at in a binary search is **proportional to the height of the tree**

If the tree is busy, then the height is logarithmic to the number of data, which gives a log time



Search and deletion are easy

Deletion is a pain



Remove a key with no child (leaf node), replace it with an empty trees / null.

Remove a key with one child, simply replace the parent with the child / return single subtree

Remove a key with two children, find the smallest node of the right subtree, remove it based on our procedures, replace it with the key that we want to remove.

We can also equally find the max node of the left subtree.





Find minimum and maximum in BST. Go down left all the way, go down right all the way.



`contains`, `add`, `remove` three basic options for BST. Basic options f or common data structure in Java.



Trim the tree into skinny tree (basically a Linked List), inserting and deletion are proportional to length of list. The operations will slow down considerably after being trimmed.

This is a performance problem with BSTs.



We want to keep the search tree bushy and balanced, which is what we need for fast retrieval



### Quadtrees

Search trees could be beyond binary

Quadtrees can divide and conquer index information about 2D locations so items can be retrieved by positions.

A quadtree is 

* Empty
* An item at some position (x,y) called root
* and four quadtrees, each containing only items that are northwest, northeast, southwest, and southeast of (x,y)

Divide 2D space in to 4 quadrants and store items in appropriate quadrant

We know the coordinate of the point we are currently and we are looking for. So we know how to search down.

Or you can use point-region quadtrees, using a bounding rectangle B

- zero up to a small number of items (2) that lie in that rectangle,
- four quadtrees whose bounding rectangles are the four quadrants of B all of equal size.

Direction are relative to the origin of the quadrant.