# Lec 24 Hashing 

Linear search is slow, can we split it into different smaller searches?

Break up collection of items into buckets. 

If the number of buckets stays within a constant factor of the total number of items in the collection, 

every search can be very quick.

As long as you can find the right bucket quickly and we can keep the number of items in each bucket near constant, everything should go very quickly. 



### Hash Functions

Which bucket something is in?

Number of bucket for the item you are looking for if that item is present.

If the item is in the table, it is in the bucket that this hash function gives you.

Otherwise, it is not in the bucket that this hash function gives you.



 ### External Chaining

Array of M buckets

Each bucket is a list of data items.

Not all buckets have same length, but average is number of items / number of buckets which is the **load factor**.

You want to keep the buckets more less equally filled, similar to keep a tree bushy.

Using a hash function with high probability to smooth out the distribution of items to buckets so no one bucket gets too large.



**Open address hashing** (no chaining)

Idea: Put one data item in each bucket.

Put all the items in a single big array.

Collision: two different keys going to the same bucket.

When you have a collision, then you just find another bucket in some systematic way. (linear probing with warp around, quadratic probes, double hashing)

Searching process is more complicated. Things can be quite slow as you become closer to full.

For linear probe: If item not at immediate place, keep going. If hit a empty item and you haven't find the item, item does not exist.

Deletion is more complicated.



**What happens when the table is filled?**

We grow in such a way that we keep the number of buckets some constant factor of the number of items.

The trick is to grow the table depending the current number of item.

If load factor gets higher than some limit, you increase the number of buckets (that change the hash functions with the extended range).

You also have to re-hash the existing items and re-stick them into the table.

Double the size of hash table every time for resizing, you get **amortized** time just as an `ArrayList`.

We want hash function to be good, constant time, and has little collision relative to the load factor.



Collisions are inevitable, but the question is whether if you have too many collisions.



**String hashing**

A string of s0s1sn-1

Simply adding them together will result in normal distribution due to CLT.

Java does this `h(s) = s0*31^n-1+ s1*31^n-2 + .. + sn-1s`. computed modulo 2^32 in Java int arithmetic

To convert to a table index from 0 to N-1, compute h(S)%N for N not a multiple of 31

Choose 31 instead of 32, for letting each of the character gets some contribution to the mix

```java
int r = 0;
for (int i = 0l i < s.length(); i+= 1){
    r = (r << 5) - r + s.charAt(i);
}
```



**hashing other data structures**

Handle ArrayList and LinkedList. Similar to string as string is just a list of characters. 

Defined on all objects called `hashCode()`.

`hashCode = 31*hashCode + obj.hashCode()`

If your hash function is taking too log, you can avoid looking at the entire list. Ex. random, only few items.

You might get more collisions. But you want to make sure that **equal thing do not give you different hash code.**

`.equals()` and `.hashCode()` are related.



For Trees and other recursively defined data structures --> recursively defined hash functions

`return someHashFunction(T.label())^hash(T.left())^hash(T.right())`



### Identity Hash Functions

By default, object provides pointer/address/reference type integer as `.hashCode()` for `Object`.

Stanford definition of `equal()` for `Object` is that the pointers are equal, just like `==`.



You can use the address of object ("hash on identity") if distinct (!=) objects are never considered equal. (exception includes String)

This Identity Hash Function is perfectly good as long as you have not re-defined `equals`.



**What should the load factor be?**

Low load factor, rather large table

What's the balance? 

Time for resizing the things depend on table size.



**Java Implementations**

`Object` has function `hashCode`, by default returns the identity hash function

Can override for your particular type, for `String`, all kinds of`List`

`HashTable`, `HashSet`, `HashMap` use `hashCode` to give you fast look-up of objects

`HashMap` has these methods `put(key, value)`, `get(someKey)`, `containsKey(someKey)`, `keySet()`

Python does this differently. Not all objects have `hashCode`, `dict` only allows the ones with `hashCode` to be used as keys.

`HashMap` in general is that they are not really good at range queries.



**Special Case: Monotonic Hash Functions**

Monotonic: either nonincreasing or nondecreasing

if Key k1 > k2, then h(k1) >= h(k2)

Useful for time-stamped records with time as key, one bucket per hour; easy for range queries.



**Perfect Hashing**

Coming up with a function that is tailor-made for that particular set of things, which provides perfect hashing.

At least 1 bucket per item for the table; # buckets >= # items

At most one item each bucket, so no collision

No searching along the chain. Either element at the hash value is equal to the key, or does not exist in the table.

We have a fixed set of things, so we can get all items gave different hash with some tweaking.

A tailor-made hash function might then hash very key to a different value.



### Characteristics

Assuming good hash function, add, lookup, deletion take **theta(1)** time, amortized (account for add)

Good for cases where one looks up *equal* keys, bad for range queries.

Hashing is not a good idea for small sets that you rapidly create and discard, as creating HashMap produces some space overhead. Use a linear sequence instead.



![Search Structure Time](C:\Users\simon\OneDrive\Desktop\CS61B\Notes\search-operation-time.PNG)