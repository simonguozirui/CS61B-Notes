# Lec 18 - Sequences, Some Design Patterns

It is hard to pin down a constant for something.

Economize on your code size. 

Project 2. Big chunk of code adopting algorithm from the book or lecture notes to real program.

How do I make it last work? "Creative laziness"

 ### Amortized Time

On average, the time taken will be O(N).

If you stop the program any time, the program takes also O(N).

The average time for each additional addition is a constant.

This is called **amortized constant time**, spread out the cost over the entire operation of the program.

Time bounds are very pessimistic. In case of interest, the amortized time bounds are much less than the actual individual time bounds for the worst case.

Sometimes the worst case can be compensated for making way for a bunch of easy cases.



The resizing cost are doubling, but the number of free operation also increases.



Each Linked List item takes up more space than array item.


Our estimated time should always be greater than or equal to the actual time

The estimated time is going to be constant (amortized) time.



How can you demonstrate this?

Show that our "bank account" (potential) for time is always positive.

Every time we perform an operation, deposit amortized cost, take out actual cost.

potential (i + 1) = potential (i) + (ai - ci); ai is amortized cost, ci is actual cost

We have saved up enough time to cover the expensive operation.



ci = 1 if i is not a power of 2

ci = 2i + 1 otherwise to account the cost of doubling.

ao =1 , ai = 5 for i > 0. 

phi (i + 1) = phi (i) + (ai - ci)

potential phi is always positive

So that anytime I stop the program the average cost of total operations will remain to less or equal than a constant.



ArrayList are good for adding to the end, not so good at adding in the middle (we cannot amortized)

Finding is fast, insertion is slow (we need to move things over)

LinkedList add in the middle. The time of actual insertion is quick, but the time to find where to insert is O(n)

Insertion is fast, finding is slow (we need to go through the LinkedList)



## Assorted Topics

### Views

Sublist in Java does not copy the list, it shares the data with the original list.

Effect will also be seen in original list. (for example, clear)



### Maps

A kind of Modifiable Functions, from one type to another

You can also get views of maps

`keySet`, `values` (multi set, possible have duplicates), `entrySet`

 

One way of thinking about a function is a set of ordered pairs



Tree Map is a sorted map, things are ordered.

View is a concept to describe some kind of data object that you have created.



Template Pattern

Certain operations maybe defined related to each other

Use `private static class ` for inner class of methods inside an abstract class.