# Lec 33 Graphs, Introduction, Traversals

Graphs represent general networks of things, objects connected to each other.

- Graphs represent objects and connections between them.
- Flow charts, Markov models
- Ordering between files (MAKEFILES, what objects do you need to build before building that one)
- Connected structures (ex `Git`)

Uses: 

* connecting roads with length
* order of things must be complete before moving on to the next, node labels how long they take
* genealogy, parent-child relationship
* Edge can represent relationships
* Represent `states`, conditions or situations of some system. Edge can be the probability of the next state, or the next state in a state machine by different input.



### Terminology

Graph consists of

* `nodes` or `vertices`. Set of nodes, `V`

* `edges` , each connects 2 vertices. 2 vertices are adjacent if there is a edge between them. 

  * Set of edges, `E`.
  * If edges have order (starting node and ending node), directed edges and we have a directed graph (digraph)
  * If edges have no specific order, it is undirected graph
  * When an edge touches a node, it is incident to their nodes.
  * Directed edges exit one node and enter the next.

* nodes or edge may have labels or weights attached to them.

  * could represented distances

* `cycle` path from a node back to itself along a sequence of edges without repeating an edge.

  * If a graph contains such a path it is cyclic.
  * No such cycle, graph is acyclic.

* Directed Acyclic Graph - `DAG`

  

### Trees and Graphs

Trees are graphs

A graph is a more general form of tree.

A graph is `connected` if one node is reachable from another.

A `DAG` is a tree if it is connected and every node has exactly one parent.

A connected, acyclic, undirected graph is also called a `free tree`.



### Representation

Assume numbered nodes.

1. Each node contains a list of its successors and predecessors.
2. Save the set of ordered pairs for edges
3. Adjacency matrix, representation of connection with matrix entry. From row to column.
   1. To get to nodes reachable in 2 timesteps, we square the matrix (which represents nodes reachable in one timestep)



### Traversing a Graph

Can't use recursion because of possibility of cycles and in case of DAG (repeated traversal of nodes) which is combinatorial explosions. theta(2^N)

We want to visit each node once.

We use mark to mark nodes.

* pre-order: mark it, visit node,  traverse its successors
* post-order: visit node, traverse its successor, visit node
* Only executes if node is unmarked.

This is a linear algorithm.



Visit all nodes. Repeat procedures, visit all nodes, as long as there are unmarked nodes.



### Topological Sorting

Given a DAG, find linear order of nodes consistent within edges. 

If we order the nodes, we cannot reach lower-number nodes from a higher-order nodes (can't go backwards)

`make` (build-control system) and PERT charts (what thing has to be done before something) does this.

Something later cannot go back to something previous.



### Sorting and DFS

**Reverse** all the links. Do a **post order** traversal, each level traverse their children, stops at an endpoint.

That means there is nothing succeeding them in the reversed graph, which means there is nothing before them in the original graph. Safe to add them to the ordering to the topological nodes.

Get rid of them and repeat, add end points to collections.

Used up all the nodes, you have visited all the nodes in the order that is the same as a topological sort.

Use the same mark traversal algorithm we used before. At visiting operation, output the node.



### General Graph Traversal Algorithm

Iterative rather than recursive; assumption of acyclic graph

```java
COLLECTION_OF_VERTICES fringe; // contains successfors of marked nodes

fringe = INITIA_COLLECTION; //set it up, starting vertax

while (!fringe.isEmpty()){
    Vertex V = fringe.REMOVE_HIGHEST_PRIORITY_ITEM();
    if (!marked(v)){
        mark(v);
        visit(v); //could be placed after traversal too, changes the order of output
        for each edge(v, w){ // look at every edge that starts at v between v and w  
            if (NEEDSPROCESSING(w)){
                add w to fringe;
            }
        }
    }
}

Replacing pseduo methods specific to algorithms.
```



Use this algorithm in topological sort.

Start with nodes that have no predecessors (add to fringe) [candidates to be out	put]

Pop one of the fringe. Look at all successors, decrement # of predecessors for each one. Add nodes with 0 predecessors to the fringe.



**Summary**

1. Look at number of predecessors each node have
2. Choosing to put them in the fringe if count = 0 (and output the node at this step), pulling them out of the fringe as we go along
3. Decrement predecessors count of the nodes they point to.
4. Continue this process until end
5. The output result is a topological sort



In the case of cyclic graph, the marked property prevents cycling. The depth is also defined here. DFS still works, as far as I can go without running into yourself. Depth depends on where you start and what order you want to traverse the successors.

