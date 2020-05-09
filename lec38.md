# Lec 38 Compression (extra material)

Threads are also an abstraction for building program (creating a particular kind of module for a program.)

**Coroutine** different then subroutine; call from time to time, when it is done, it gives you back the control.

Mailbox idea: deposit and withdraw messages

Tree Iterator and Tree Professor

every now and then call receive of the mailbox

Using parallel control construct to create a control structure for an iterator to go through the tree.

This way is similar to python generator.

It has no assumption of what the program is going to the node that you find. Don't have to worry about states.

Leave the recursion temporarily, user take value. Processor processes the value.



**Java uses threads for GUIs**

Event thread. 
Main thread, starting everything else.

Designate an object to be an listener. 

GUI registered itself as a listener. Whenever the model changes, the GUI can respond to it.



**Interrupt** an event that disrupts the normal flow of control.

Interrupt can be totally asynchronous.

Remote Method Interface (remote procedural call): one java program executes on one computer, and then another on another computer. They can coordinate with each other, seem like they are calling a shared methods of an mutual object.



Proxy for an object through I/O operation , through serialized (turned into a stream of bytes and back).

`RemoteException` (subtype of `IOException`)



### Scope and Lifetime

Where in a program is a particular declaration applicable.

Ex. scope of local variable declaration.

In Java, every scope of the declaration is **static**, it is independent of data.

**Lifetime** or **extent**, the length of storage execution which it exists.

Classes of extent:

* *Static*: entire duration of program
* *Local* or *automatic*: duration of call or block execution (local variable)
* *Dynamic*: From time of all allocation statement (new) to deallocation, if any. (You can't tell from the program, you have to see how the program executes)





There is no way in Java for free this storage.

If there is no way that your program can mention that object, the object is useless.

Everything happen to it is irrelevant to the program.

When needed, it can find that useless object and recycle to use those to save memory space.

This is called **garbage collection**

These are all integer addresses into machine's memory.



**Allocation**

Java cannot convert between integers and pointers both way.

C can do it both way. These conversions cause the runtime to be corrupted, making it **unsafe**.



OS gives away to turn chunks of unallocated region into heap. This happens automatically for stack.

```
- Stack (grows down)
- Unallocated
- Heap (grows up)
- Static storage
- Executable code
```



**Deallocating**

Explicitly deallocate, the computer has to trust what you are doing. (C programs have a lot of those problems, such as memory corruption, memory leaks).

Free List to keep track of memory you have freed and available for allocation.

