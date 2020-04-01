# Lec 26 Sorting

Sorting algorithms

* Support searching (ex things have to be in order for binary search)
* You can answer 
  * if two items equal in this collection (sort and becomes linear time problem)
  * Sort things based on same properties
  * What are my nearest neighbors?
* Convex Hull problem: sort the points by angle regarding a central point



Sorting algorithm (sort) permutes (re-arranges) a sequence of elements to brings them into order, according to some total order (every 2 elements are in some kind of order).

Total order -<, total, reflexive, antisymmetric, transitive.

Some ordering may treat unequal items as equivalent. Consider two entries equivalent in the sort even they are different.

What order does equivalent things appear in a sorted order, might as well obtain the original order they are put in. A sort that does not change the relative order of equivalent entries (compared to the input) is called **stable**.



**Classifications**

* `Internal sort`: keep all data in memory
* `External sorts`: process large data in batches, some data resides somewhere else (cloud, disk)
* `Comparison-based` sorting depends on the this question: is this item less than that item? Only info uses is whether one thing is less than other
* `Radix` uses more info than just comparison.

Strategy

* `Insertion sorting`: build up result by sticking items into it. As you go, you keep the result sorted by inserting the item at where it should be.  Slip it at the right thing
* `Selection sorting`: find the smallest, stick it in; find the smallest now, stick it in.



**Java primitive types sorting array**

For primitive type P

`static void sort(P[] arr) { ... }`  sort into non-descending order

`(P[] arr, int first, int end)` a portion of the array.

From first not including end. All the other elements is untouched.

`static void parallelSOrt(P[] arr) { ... }`

**Reference types sorting Array**

Reference types have a natural order.

`static void <C extends Comparable<? super C>> sort(C[] arr) {...}` using the natural order

`static <R> void sort(R[] arr, Comparator<? super R> comp) { ... }` Supply your own sorting order.

Use a sub list method of `List` using a view of the list to sort a portion of the list.

**Reference type sorting List**
Similar to Array

`void sort(Comparator<? super R> comp){ .. }` in the **instance** method (included in List<R> interface)

`sort(x)` 

`sort(x, (String x, String y) -> {return y.compareT(x);})` reverse order (using Java lambda function to create a new comparators)

Comparator object `Collections.reverseOrder()`



### Insertion Sort

Start with empty sequence of outputs

Add each item from input, inserting into output sequence at the right point



Simple and good for **small** sets of data.

With vector (vector: array, arrayList,) and linked list, time to find the place to insert and insert of one item is at worst theta(k) where k is number of outputs so far. 

theta(N^2) algorithm in total (worst case)

1 + 2 + 3+ 4 + 5 + 6 + --- + N == N^2



### Inversions

Pairs that are out of order

theta(N) comparisons if already sorted

If all items within K of proper places, then takes O(KN) operations, where K is a small constant

Thus this is good for nearly sorted data.



N^2/2 for large K

How can we measure what is nearly sorted? # of inversions: pairs that are out of order

When it is perfectly sorted, this is 0.

When it is in reversed sorted, this is N(N-1)/2



Total time of the loop executed depends on number of inversion.

Sorting time: size of array + number of inversions



This algorithm take N^2 type in the worst case





### Shell's Sort

Compare elements that are far apart from each other.

Find far apart out of order, then you make in order, then you decrease # of inversions in quite a bit.

(2^k - 1) is a convenient choice as you want to make the distance smaller

First sort item some multiply (2^k - 1) apart.

Now sort (2^(k-1) - 1 ) apart

....

Now sort (2^0 = 1) apart, but most inversions gone.

This sort is theta(N^(3/2))



2^k is the initial size, 2^k - 1 is the last index

