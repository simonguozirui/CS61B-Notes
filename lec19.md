# Lec 19 Sequences (II)

 When you plug in `size()` and `get()`, supply you `contain` and `iterator`

 Iterator has `next()` and `hasNext()`



`private static class` inside an abstract class

Because you know the interface still have those methods, you can still access them.



Another approach is to create an inner class

`AbstractList.this` means "the AbstractList I am attached to".  You can leave this part out as it is unambiguous

`X.new AlistIterator` means "create a new AListIterator that is attached to X". You can do `this.new` if unambiguous



Read the existing list in reversed view

`ReverseList` class does not know the details of List (the kind of List it is dealing with, no knowledge of implementation), but just relying on the methods that List have.



### Arrays and Links

Two main ways to represent a sequence are Array List/Vector and Linked List

Array List

* Efficient use of space
* Very fast at random access (index), constant time operation
* But deleting and inserting can be slow, theta(N)

Linked List

* Insertion and deletion is fast as long as you find where you want to do it
* But there is a higher space overhead and slow random access



### Implementing with Arrays

Adding and removing at the end is easy

How can we make it fast to add/delete at the front and the end, while still maintaining random access?

Use **circular buffering**

Not necessarily first element at index 0. That way we allow easy delete and add at both ends while maintaining a fast random access.

Array is full: last pointer + 1 = first pointer modulo size of array. 

Will be an issue if you have an empty array, because it looks full

Won't be a problem if you use the size of array stored separately as the property of Array List

There is a java implementation `ArrayDeck` of this that you can cheaply expand and contract an list on both sides.



### Link

Linked List interface and Array List interface looks similar

To count for null case, we do not contain list of items, but contain a pointer to the list of items

Link object links a **sentinel node**, a dummy object at the start and end of the list

The list starts to the right of the sentinel node, ends to the left of it

By doing this, we avoid empty list as a special case, hence making everything general

Empty list will then just be the sentinel

Avoids conditional check that otherwise you need to do.



Sentinel is a dummy object containing no useful data except links

Ensuring that first and last item of a list always have non-null nodes before and after them



### Specialization of Lists

* Stack: add and delete from one end (LIFO: last in first out)
* Queue: add at the end, delete from the front (FIFO: first in first out)
* Dequeue: add or delete at either end

Usually represented by either array (with circular buffering for queue or deque) or LinkedList

ArrayDeck allow you to add and remove from both ends very swiftly



### Stacks and Recursions

Stack is a subtype of List, but there is no interface for it

Stacks are related to recursion.

Convert any recursive algorithm to stack-based algorithm

Procedure call data structures are stack like

Control structure converted into data structure



### Design Choices: Extension, Delegation, Adaptation

 You can create a stack like structure 

* **Extends** `vector` and override functions
* You could **delegate** the data to a field
* You can define an **adapter**, a class used to make objects of one kind behave as another. Create ArrayStack by extending the adaptor class hence inheriting its methods. Treat the object as it behaves like stack. The object basically adapts another object to a new particular interface. This is more general and you can apply it to more things. 











