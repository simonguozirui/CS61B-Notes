# Lec 36 Dynamic Programming, Enumeration Types

A **general distribution** between two finite bounds.

Distribution function: a probability at any time for a random number being less than equal to a value

Produce random number according to normal distribution.

For each point on the distribution, find the inverse, the value that produces that.

Figure out how to produce distribution functions --> invert the distribution function, and use those values to produce them. It is possible to get any thing.

**Java Implementation**

`Math.random()` random double in [0, 1)

`java.util.Random`, `Random()` seed based on time, `Random(seed)` reproducible

`next(k)`, `next{Type}()`

`Collections.shuffle(L,R)` for `list l` and `Random R` permutes list L randomly using L

**Shuffle** 

start from the end, swap the element with any item before it selected randomly.

**Random Selection of K elements of List L**

Shuffle the whole list, return a sub list. Time depends on length L of list. (not efficient)

**Floyd Algorithm** - alternative selection algorithm

Add `random number j` if not in set yet, or else (if repeated) add `index i`.



### Dynamic Programming

Recursive programs can cost a lot of time. 

**Memoize** save a lot of intermediate results to avoid re-computation.

Number of recursive calls drop from 2^N to N^2 in the example given.



Usual presentation of dynamic programming is iterative.  

That is, we figure out ahead of time the order in which the memoized version will fill in memo, and write an explicit loop.

This way saves the time needed to check whether result exists. 



If your space is constrained, memoize; otherwise, don't bother.



Longest common subsequence: Discard the characters from both string.



Memoizing decrease time from **exponential** to **polynomial**.