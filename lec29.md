# Lec 29 Sorting (III) 

So far, everything is N^2 or NlogN we looked at.

For any algorithm addressing a particular problem, what is the lowest worst-case time you can get?

**Lower bound on the worst case** of the algorithms available for that particular problem, which one is the best?

 Can we do better than `NlgN`?

The lower bound/best worst case you can get for any algorithm with only allowing moving and comparing operations, is proved to be `NlgN`.

N input, N! combinations of data, N! different combinations of data-moving algorithms, any algorithm have to go through the height of a decision tree.

If we make k tests, you get 2^k outcome (number of different decisions), we design it to make 2^k >= N!

k is omega(lgN!) which is roughly `theta(NlogN)`, worst case for any algorithm



## Beyond Comparison, Distribution

Have set of N integers, value between 0 and kN, for small constant k

Use **distribution sorting**: (assume no repetition)

* Put integers into N buckets, integer p goes to bucket [p/k] (rounding down), theta(N)
* Per bucket at most k keys. We can concatenate them and do insertion sort on them as they are almost sorted, theta(kN). 

In total, theta(N)



**Distribution Counting**

Data that might have some repetition.

If Mp = # of items with value < p, then p is at Mp's index of the array.

The count of numbers < k gives the index of k in the output array.

If there are N items in the range 0 ... M -1, gives another linear-time theta(M+N) algorithm, add both values to account for duplicates.

Have three lines: counts (# occurrences of each key), running sum (cumulative count of keys < each value, or where to put the keys), next positions (keep track of the position of the next key value should be at)

Use the first line to generate second and third. Use third line to update the output based on the input, and updating itself as well.

These are all linear time operations.



Why do we care about duplicates? We usually sort key, the key part of records that contains all sorts of other information. So there are cases of duplicate keys.



### Radix Sort

LSD (least significant digit) radix sort. Each of these sorts are **stable**.

For a 3-letter case.

Sort them letter by letter, starting from the last letter for each, and then sort the data based on that using distribution sorting.

Create a new list using concatenation. For each bucket, we maintain the original order within the same bucket, thus remain stable.

Repeat --> distribution set by index one left, construct new list --> .. --> distribution sort by the first letter --> sorted list.

Stabling sorting the list that is in order by the second character and for each equal second character in the original order with respect to the last character. Thus everything is already in order by the second andthird character.



MSD (most significant digit) Radix sort 

Not looking at all the data as much as the other one.

Once it divides into regions by the digit, those items stay in that region.

A bit more complicated: must keep lists from each step separate.



### Performance

Takes theta(B) where **B is the total size of key data** in bytes

It is linear of the total size of data. 

B = NlgN time with minimal-length keys. But it might not have a good constant factors.

In general, your length of record will be longer than your minimal length key. Do consider how long the key is on how much data you need to deal with.



You must have theta(logN) keys for N different records. Comparison takes theta(K) where K is size of key in worst case. 

Thus, the NlgN comparison should really be [NlogN comparisons * logN operations per comparison]





### Search Trees

Search tree is in sorted order. 

Put things in to BST

If the tree is **balance (bushy)**, you can do an in-order traversal. 

You will have N insertions in time lg N each plus in-order traversal take theta (N)

The performance will be the same as heap sort. Theta(N + NlgN) = theta(NlgN)





### Summary

| Sorting Mechanism | Worst Case in Theta                                          | Best Case in Theta | Implementation and Advantages                                |
| ----------------- | ------------------------------------------------------------ | ------------------ | ------------------------------------------------------------ |
| Insertion Sort    | `Nk`where k is max amount data displaced from final position, or `N + #inversions` | same               | Good for small dataset, or almost in-order data. Good constant factors. |
| Quicksort         | `N^2` (pathological dataset)                                 | `NlgN`             | Good constant factor unless data is pathological causing algorithm to pick the wrong pivot. |
| Merge sort        | `NlgN` (Guaranteed)                                          | `NlgN`             | Good for huge dataset. If you can't fit in computer memory, you can break it up and handle each chunk separately, |
| Heap sort         | `NlgN` (Guaranteed)                                          | `NlgN`             | Priority queue                                               |
| Tree sort         | `NlgN` (Guaranteed)                                          | `NlgN`             | BST and in-order traversal (assume good balance, need guaranteed balance) |
| Radix sort        | `B` (number of data of the key in bytes)                     | same               | Rely on more info than  just comparison of keys. Good for external sorting. |
| Distribution sort | `B` (number of data of the key in bytes)                     | same               | Good for external sorting if you can afford to keep buckets in memory. You can also output data of the buckets in files (one file per bucket). |