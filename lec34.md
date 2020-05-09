# Lec 34 A* Search, Minimal spanning trees, Union-find

### Dijkstra's Algorithm

Single point shortest path.

A weighted graph, find the shortest path from a given starting point S to all the nodes in the graph.

We assume all non-negative weights.

"shortest" = sum of weights along the path is smallest possible

**Idea**: keep an estimate of how far each node is away from s, also keep track of how we get to that node (preceding node in shortest path from s). 

The algorithm updates the estimates as we go along thus increasing number of shortest path we computed.

**How to update:** Our fringe is a priority queue based on the estimated distance of each node from the starting node s.

```java
PriorityQueue<Vertex> fringe;
For each node v { v.dist() = inf; v.back() = null;} // initial conservative estimate
s.dist() = 0; // the only known distance from s, rest are all estimates
fringe = prioirty queue ordered by smallest .dist(); // contain all the nodes, make sure there is no better way to get a node

add all vertices to fringe;

while (!fringe.isEmpty()){
    Vertex v = fringe.removeFirst(); // popped is processed and final.
    // look at all v's neighbour, w
    For each edge(v,w){
        if (v.dist() + weight(v,w) < w.dist()){
            // update w's distance and how we get to w
            w.dist() = v.dist() + weight(v, w); w.back() = v;
            /* In real implementaion, since it is in a priority queue, for updating w, we need to remove it from the fringe, update its dist(), and add it back to the fringe. */
        }
    }
}
```

We can ignore anything that has already been processed. 

This algorithm finds node in the actual order that they are closest to the starting node.



Backward arrows indicating by the shortest mean how you can get to a node from the start.

The backward dashed lined arrows (indicating the shortest path tree) is a DAC!

The shortest-path forms a tree, which is called the shortest-path tree.



You can like each edge at most twice in this algorithm!
You usually have to look at all the edges.

It is quite efficient. No need to prune.



Negative numbers are disallowed as you can create cycles and get to infinitely negative numbers.



Enhancement of Dijkstra's Algorithm

### Point-to-Point Shortest

Dijkstra's Algorithm is a single-pointed shortest path problem

You can run Dijkstra's Algorithm until you pick the destination point, but inefficient.



### A* Search

 Make a careful heuristic guess h(V) of length of path from any vertex V to any destination.

Instead of visiting vertices in fringe by estimated distances, we also add in the heuristic estimate distance to decide the order of our visits.

`d(from, V) + h(V)`

we look at places that are reachable from places where we knew the shortest path to `from` and choose those that look like they will result in the shortest path to `destination`, guessing at the remaining distance. 

This will point us to the right direction.

**What are our heuristics?**

The heuristic cannot be too large. It needs to be **admissible**; `h(C)` must never overestimate `d(C, destination)` If it is too big, we will not get the shortest path necessarily.

On the other hand, if it is too small, it will work but it won't be a good heuristic. 

Also needs to be **consistent**, `h(A) <= h(B) + d(A,B)` triangular identity



You stop when you get to destination. 



### Summary

**Dijkstra's algorithm** finds the **shortest-path tree**. It compute backwards shortest paths in a weighted graph from a given starting node to all other nodes.

Time required = time to remove V nodes from priority queue + time to update all neighbors for each of these nodes and add or reorder them in the priority queue. (`ElgE` due to heap structures)

`Theta(lgV + ElgV) = theta((V+E) lgV)`

* `lgV` time to update an edge.
* `E` factor to do this for every edge
* `V` some cases to ensure we cover all cases



**A* searches** for a shortest path to a particular target node.

Similar to Dijkstra's, except

* stop when we take target from queue
* Order queue by estimated distance to start + heuristic guess of remaining distance
  * `h(v) approximates to d(v, target)`
* Heuristic must not overestimate distance and obey triangle equality.
  * `d(a,b) + d(b,c) >= d(a,c)}`



### Minimum Spanning Tree

Given a set of places and positive distances between them, find a set of connecting roads of minimum total length that allows travel between any two.

The routes you get might not be the shortest paths.

It will form a tree in the end, it is an acyclic undirected graph.



### Prim's Algorithm 

* Grow a tree from an arbitrary node.
* At each step, add the shortest edge connecting some node already in the tree to one that is not yet.

```java
PriorityQueue<Vertex> fringe;
For each node v { v.dist() = inf; v.back() = null;} // initial conservative estimate
s.dist() = 0; 
fringe = prioirty queue ordered by smallest .dist();

add all vertices to fringe;

while (!fringe.isEmpty()){
    Vertex v = fringe.removeFirst(); // popped is processed and final.
    
    /* PART DIFFERNT THEN Dijkstra's*/
    For each edge(v,w){
        // w make sure hasn't been processed and added to the MST
        // its distance is greater than the weight of edge vw
       if (w in fringe && weight(v, w)<w.dist()){ 
          
           {w.dist() = weight(v,w); w.parent() = v;} // not adding current distance
       }
    }
}
```

After this, we have a tree. the minimum spanning tree. 

The sum of length of the edges is the minimum possible sum.

This works because: 
It isn't going to help you to go around the tree in some other way, because the bottom line is the distance I have to travel to connect myself to everyone else, is determined by the minimum weights of edges that gets  to that tree.