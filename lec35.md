# Lec 35 Pseudo-Random Sequences

### Minimum Spanning Trees by Prims' Algorithm

* Minimum Spanning Trees: a tree contain all the nodes of the graph, not necessarily all edges, with minimum weight
* Grow a tree starting from an arbitrary node
* Update all the pointer to point backward from connected nodes.
* Add another node that is closest based on estimated distances (weight of edge).
* Repeat. Update this if closer to the tree. 
* When we are done, we have a tree (node pointing all the way to the parent). Properly give you a tree.

Very similar to Dijkstra algorithm. Iterate once per reach a node.

Update node, remove from fringe and reinsert.

LogN time for each move. 

Overall, elog(e) bounded by log(v) ; e = edges, v = vertices.



### Kruskal's Algorithm

Idea: takes the shortest edge of the graph as it is always part of the minimum spanning tree.

Create a subtree for each node in the graph. V nodes, V subtrees.

We take all of the edges, sort them in order of **increasing** weight.

Take the lowest remaining weight, add the node into collection.

Combine the two subtrees into one if already not connected.

```
if (v,m) connects two different subtrees: [Find]
	add (v,w) to MST
	combine the two subtrees into One [Union]

```

Also called union-find algorithm

**Find**

Which tree is a node in? Follow the pointer along one root. 

Always able to identify the subtree by the root of subtree.

Could be slow as they could be quite long and stringy.



**Combined**

Add one arrow from the root of one tree to the root of the other root

In order to union, you fist have to find the roots (representative of the 2 subtrees).

Constant time operation after find algorithm.

Choose the root of the larger tree as the union representative.



**Long stringy path, can we do better?**

Path compression.

When we find, we take all the nodes along the path directly the root.

Flatten the structure.

Every subsequent operation will be short. 

**Amortized time**: a sequence of find and union. Near **constant** amortized time.



### Pseudo-random Sequences

You can get random number in computer with special hardware or unique network methods (listen to #packets)

Pseudo-random Sequences can be really quickly generated

Used for

* statistical samples
* simulations (introduce randomness)
* random algorithms (skip lists)
* cryptography **very important**
  * Secure web communication. Come up with keys that can't be guessed since they are long random numbers if they are random enough.
* games



### Random Sequence

Not too strong definition: An unpredictable sequence where all numbers occur with equal frequency

A "truly" random sequence is difficult for a computer or human to produce

Computer use some sort of entropy

Sequences need to be hard or impractical to predict

**Pseudo-random sequence**: deterministic (reproducible) sequence that passes some given set of statistical tests (look at lengths of runs)



**Linear congruential method**

X0 = arbitrary seed

Xi = (aXi-1 + C) mod m, i >0

`a`, `C`, and `m` has no common factors; or else you won't get values in between; ` a ≡ 5 mod 8`

Good potency measures certain dependencies among adjacent xi

Java's implementation is good enough, but not cryptographically secure.



If we choose it wrong, we get short sequences. could be problematic.

bad potency leads to bad correlations.



**Additive Generators**

Get a long period. Simply implemented by circular buffer.

Adding previous terms. Starting out with some pseudo-random seed.



**Cryptographic Pseudo-Random Number Generators**

Properties

* Given K-bits, no polynomial-time algorithm can guess he next bit with better than 50% accuracy.
* If state is leaked already, infeasible to reproduce.

Implementation

* start with a block cipher
* as a seed provide a key, K, and an initialization value I.
* AES
* the jth pseudo-random is now E(K, I + j), where E(x, y) is the encryption of message y using key x.



We can adjust range and distribution.



Make sure you are not biased for the last number.

If we get a number that is larger than maximum, we will try new ones.



**Thus, we can generate arbitrary bounds**

we can get things between range of 0 and n-1, scale it and then add L, we can get range between L and U.

Random Float `d*nextInt(1<<24) / (1<< 24)`

