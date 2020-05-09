# Lec 28 Sorting (II)

### Sorting by Selection: Heap Sort

Use of priority queue.

Select member of the output one at a time, from largest to smallest

Using array representation of heap.

Heapify, remove the largest and then re-heapify.

Add the removed number to the sorted array.

**O(NlgN)** - N remove-first operations

A **bad** idea for simple list or vector.



### Initial Heapifying

Faster procedure then insertion in empty heap N times

Start from N/2.

Bottom layer heap property is satisficed.

We go back along the heap to the top, everything below us are properly re-heapified.



Certain number of heapify bubble down operation.

Theta (N) for the sum.

2^0*h + 2^1*(h-1) + .. 2^(h-1)*1 = theta(2^h) = theta(N)

Since the rest of heap sort is still theta(NlgN), so this does not improve asymptotic cost overall.



### Merge Sorting

Divide data in 2 equal parts; recursively sort halves; merge results

theta(NlgN)

Good for external sorting, where you have too much data so you can fit in memory and sort.

Merge K sequences together and we have theta(K)

With very little space we can sort things very quickly.



**binomial comb** to add slots of pairs and merge them when slot is occupied

Can include Linked List to make it more space efficient



In place merge sort hard to sort them together.

Either the place is empty or contain a maximum length for that slot



### QuickSort

In usual case it is pretty good.

Partition data into pieces, everything > `pivot` value at high end of the sequence to be sorted, everything <= are on the low end.

Repeat this recursively on the high low pieces.

For speed, when the pieces are small enough (length under a certain number), we stop and do insertion sort on the whole thing.

Because insertion sort is a linear time operation on almost sorted array. Everything is closed to where it should be.

How do we choose to pivot well? we choose the **median** of first, last and middle items of sequence.

**good pivot** divide data in two, theta(NlgN) [BEST CASE]

**bad pivot** most items on one side, theta(N^2)



When the sequence is almost sorted, use insertion. When not, use quicksort.

Randomly shuffling the data before you sort makes omega(N^2) time is very unlikely. Make the algorithm faster by shuffling the data.



QuickSort usually have better constant factor than HeapSort, tends to be faster. Probability of N^2 is quite low. The time bound is not guaranteed.



### Quick Selection

How to find the kth smallest element?

Not good: Can we sort, select element #k? theta(NlgN)

Instead, Partition around some pivot as in quicksort, make the pivot at the dividing line.

See where around the final sequence of the array you want lie relative to the pivoting points.

See where kth element lies on the pivot's left or right.

Reduce to a small size and then just sort it. Most of the array is unsorted but you find it.



We get theta of N if we assume we can evenly divide the arrays.

It might be N^2 as evenness is not guaranteed.



