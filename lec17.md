# Lec 17 - Collections, Amortization

Ignore the small sizes, look at as the overall shape of the function as opposed to any particular values.

Nested loop more complicated, often lead to polynomial bounds.

Asymptotic time unchanged by constant factor.

Just because it is 2 nested loops, does not mean it is O(n^2)


Exponential searches, exponential time avoid at all cost.



Binary search: slow growth. Example show log scale.



Write out the cost function expression, categorized by time.

Merge sort: 

Make N = 2^k, but the case stands for any arbitrary N

C(N)  = 2C(N/2) + N

The number of times you can divide N by 2 --> lg N



Naïve sorting algorithms N^2, NlgN is a significantly improved approach



### Java Collections classes

Data structures that contain things

6 interfaces in the `java.util` library to represent collections of objects

* `Collection`: General collections of items
* `List`: Indexed sequences with duplication
* `Set`, `SortedSet`: Collections without duplication
* `Map`, `SortedMap`: Dictionaries (key --> value)



Concrete classes: `LinkedList`, `ArrayList`, `HashSet`, `TreeSet`



Purists use concrete types only for new, interfaces for parameter types, local variables

But slower, like 10%.



Sub-interfaces are subtypes, usually have more methods, describe a smaller set of types



`Vector` very ancient, but very good for writing parallel (multi-threaded) programs than `ArrayList`; it allows multiple process to access its dat simultaneously.



`Collection`: `List`, `Set`

`Map`, separate part of the collection, not under `Collection`


**The Collection Interface**

Membership test: `.contains`, `.containsAll`

Queries: `size`, `isEmpty`

As there is no ordering in collection you need retrieval: `iterator`, `toArray` (order not guaranteed)

Optional modifiers: `add`, `addAll` (union), `clear`, `remove`, `removeAll` (set difference), `retainAll`(intersect)

Optional allows implementations to throw an exception `UnsupportedOperationException`, as not all `Collection	` need to be modifiable; often makes sense just to get things from them (Read Only).



**The `List` Interface** extends `Collection`

Indexed sequences, you can index into it.

Adds new methods to `Collection`

Membership tests (where is it): `indexOf`, `lastIndexOf`

Retrieval: `get(i)`, `listIterator()`, `sublist(B,E)`

Modifiers (where to put it or remove from): `add`, `addAll`, `set` (possible due to indexing)



Since it is indexed, it can go "forward" and "backward"

Adds `previous` and `hasPrevious`

With modifiers, you can iterate through a list, insert, remove, and change as you go.



Use `List L` than `LinkedList L` or `ArrayList L`, makes your method generally more applicable.



`ArrayList`, add an item each time by creating a new array and copying the old elements into the new array, cost theta(N^2) for N additions.

Where as adding things to `LinkedList` (if you can access the end), cost you constant time.

`LinkedList` is better for adding.

However, `ArrayList` is better at random access as `LinkedList` has to iterate through

However, `ArrayList` can be made just as fast as `LinkedList` when you add things to them.



Best thing is to do is to double (or multiply) the size of array. Proportional to N.

A lot of work and followed by many constant time work



### Amortized Time

Sequence of operation, different than single operation

Make it looks like we are taking "constant time" for each addition rather than (one expensive operation followed by many constant time operations)