# Lec 30 Balanced Search Structures

### Sort Review

**Straight Selection Sort**

Get the min or max and put them at the right index; very slow

**Standard Sort**

Things don't get entirely sorted at first, but then insertion sort them (almost at order); very fast

**Other**

Merge sort could be stable

**Bubble Sorted**

A kind of insertion sort that repetitively does swaps

**Bi-tonic Sort**
Good for parallel processes. Kind of merge sort but sorting happens in 2 directions.

**Bogo Sort**

Permuted randomly until it is in order (long)

 ### Balanced Search Structures

BST are great when bushy, how to keep them bushy

O(lgnN) performance: insertions are fast if not too deep; not too deep (bushy, node has some constant > 1 numbers of children; height reduced log constant N)

### B-Trees (B for balanced)

Not a binary tree, but a multi-key tree

Forced everything to be uniform height.

keys + 1 children for each node. The keys divides and bounds the children.

**Rules**:

1. Order M B-tree is an M-ary search tree, where M > 2; M or fewer children in each node
2. Keys are sorted in each node
3. All keys in subtrees to left of an given key, K, are < K, and all to the right are > K.

Bottom layer - empty children and leaves

How do we maintain this structure, no more than log(N) levels?



For root, all the subtrees remain the same height.

**Each node has to have at least [M/2] (rounded up) to M children, and one key between each two children.** This property allow us to split things.
Root can have less. 



**Insertion:** Insert at the bottom, if the node breaks the rule (have more than M children), we split it up.

We split up the node that violates property, select one of these cases in the middle, split it up based on the middle key, and move the key up. Repeat this process until nothing violates property. If there is no parent, create new parent.

Made the tree-deeper, but all the bottom nodes have the same height.





Which one to move up? In the middle, or if odd, choose the exact middle.



**2-4 Tree**: every node has 2-4 children. The root itself have less than 4 children.



**Delete**: Delete key, --> if node violate from property --> combine with its siblings by dropping the parents -> repetitively does this while also checking if combined node is too big so we can split.

 

### Red-Black Tree

Another representation that is related.

A BST and its node are colored red and black. The coloring of the node keep the node balance, allowing searching to always be O(lgN).

Used for `TreeSet` and `TreeMap`

To restore balance when items are inserted or deleted, tree is `rotated` and `recolored`.

**Constraints:**

1. Each node is conceptually colored red or black
2. Root is black
3. Every leaf node contains no data (as for B-Tree) and is black
4. Every leaf has the same number of black ancestors.
5. Every internal node has two children.
6. Every red node has two black children.

The last three conditions guarantees the O(lgN) search properties.

This structure ensures the amount of black nodes (which within a factor of 2 of the total amount of nodes in the tree), it mains the tree is a bushy tree. It is sufficient bushy to make things fast.

Same data-structure as 2-4 BTree.

Each BTree node corresponds a group of nodes (one parent black node and red children); all red nodes point to other groups (BTree node)



**Depth of the tree only progresses logarithmically**



### Left leaning Red-Black Tree

 Restrict ourselves to have red nodes on the left of a parent. Creating a 1-1 relationship between 2-4 tree and red-black tree.



Consider (2,3) Tree

**Insertion**: insert at bottom as for binary tree (color it red except when the tree is initially empty)

**Rotation**: preserves the BST property by changing the structure of a tree

* rotateRight():
  * left child comes to top, parent becomes its right child, the nodes in between them shift from one to another
  * Lengthen the right side, shorten the left side, might help balance things out.
* rotateLeft();



**Recoloring:** **Transfer** the color from the original root to the new root, and color the original root **red**. Maintain property for every leaf to root has same number of black ancestors.



Can't have red parent and red children!!