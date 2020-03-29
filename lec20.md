# Lec 20 Trees

Tree is a hierarchical structure that reflects a recursive description.

They have more than one recursive subpart for each instance.

Dividing data into multiple and distinct subsets that enables switching through it.

A node is a parent of its children.



Position trees: if every node has two positions, we have a **binary** tree and the children are its left and right sub-tress.

Nodes are the parents of their non-empty children.



### Tree Characteristics

root of entire tree: node with no parents

Every child of some other node is itself a root for some sub-tree.

`Order`, `arity`, `degree`: maximum number of children in a tree or a node

K-ary tree each node have at most k children.

A leaf has no children. For a binary tree, a leaf is a node that has no non-empty children.

Empty children are not counted as children!



Height: largest distance from a node to a leaf

A leaf has height 0 

A non-empty tree's height = 1 + maximum height of its children

Height of a tree is height of its root.



Depth: How far you are from the root



Useful concepts when talking about performance



`TreeSet` and `TreeMap `have no tree-like operations, but they use tree implementations, and their speed.



### Traversal

Go through the data of the tree and do something with it

Traversing a tree means enumerating (some subset of) its nodes.

Recursively or adding another data structure (for example, a stack) and use it iteratively

As they are enumerated, they are `visited`

**3 basic orders for enumeration (+ variations)**

1. Preorder: visit node, traverse its children
2. Postorder: traverse children, visit node
3. Inorder (for binary trees): traverse first child, visit node, traverse second child 

Note the difference between visit and traverse! Traverse is a process.



The order of in order is usually from left to right, but could be application-specific, as we will see in graphs later on.



**Uses of trees:** 

Expression tress. Inner nodes are operators, leaf nodes represent variable. 
Left node, right node are operands of the expression of the node (label)

- Preorder traversal (visit node, traverse its children) <--> Prefix expressions, for example (+ 1 2)
- Inorder traversal (traverse first child, visit node, traverse second child) <--> Infix expressions (1+ 2)
- Post order traversal (traverse children, visit node) <--> Postfix Expressions, Reversed polish notation: type in the two operands and see what operator you want to apply tot them



After generalize, abstract

The thing that differs from one preorder traversal and another is **what visiting means**


Give it a visitor, a use it to visit the node

`Consumer<Tree<Label>>` , consumer interface, takes a value and consumes it by yielding void

This `accept` function acts like what a function would act like in Python

Java 8, lambda expressions

`preorderTraverse (myTree, T -> System.out.print(T.label() + " "))` the second parameter input is a consumer

Take it as body of accept, create the class that implements consumer has this accept method, takes this tree, and does this to it. Figure everything out by itself.



**Iteratively**

Keep a stack of trees.

Last node in, first one out, has to be the leftmost child. Thus you push child into stack backwards.


Same time and space as recursively, but space is more explicit through the stack data field

Substitute an explicit s tack data structure for Java's built-in execution stack.



Maximum value of stack at any given time = depth * maximum variety



Binary tree has height n, has 2^n nodes.

No matter what order it is,  the time to traverse all the tree is **linear theta(N)**



One visit at the root, and then one visit for every edge/link in the tree.

We use each link at most two times, go down, come back up.

Number of links = number of nodes (N) - 1 as there are one parent link for each node, except for top root

So there are (2*(N-1)) visits



**Level order (Breadth-first) traversal**

Traverse all node at depth 0, then depth 1.

Instead of a stack, we use an `ArrayDeque` (queue, FIFO).

Push every child in order from left to right.



Empty nodes still cost time, but number of empty trees in positional trees within arity of the tree * number of notes. So we haven't really changed anything by taking in account empty trees.





**Formulas**

Number of nodes N and k-ary tree (k as height)

h+1 <= N <= (k^(h+1) - 1)/(k-1) [maximum number of nodes that you have to deal with]



height is at least (lgN) and height is bounded by O(N)



Worst case time for looking at one child only, you are operating it very linear, proportional to the height of the tree.

Bushy tree, upper hand of the range shown above, time required will be theta(N), very fast algorithm that can be used to for final searches





Turn DFS in to BFS, you keep track of how far down the tree you are, repeatedly call `doLevel(Tree T, int levk)`, visit things at that level only. We skip the nodes before level k and then visit at level k, but not their children

So we do breadth-first traversal by repeatedly (truncated) depth-first traversals: **iterative deepening**

For bushy one, it is theta(N) and for not bushy one, it is theta(N*2)