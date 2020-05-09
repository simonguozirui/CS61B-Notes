# Lec 37 Threads, Garbage Collection

### Enumeration Types

Need a type to represent something that has a few, named, discrete values

All unique distinct values, can be used to test equality. Useful for `switch statements`

Have symbolic names for constants.

```java
public enum Piece { //new reference types
    BLACK_PIECE, BLACK_KING, WHITE_PIECE, ... // final enumeration constants/enumerals of type Piece; all object of type Piece
}
```

You can easily use `==` here. They are the only values of the enumeration type that exists. You cannot create a new enum value.

You can make these enumeration static member of the static class `Piece`. You can do static import to make things simpler (but can't do this in anonymous package)



These enumerals' order matter. You can tell by `ordinal()`, sometimes useful.

List all the values. `Piece`.values() return array of all possible values.

`toString()` method and `valueOf` method to convert between String and `Piece`



Enums are classes, so you can define extra fields, methods, and constructors.



```java
enum Piece {
    BLACK_PIECE(Black, false,"b"); // only systems can create this
    
   	//fields
    
    Piece(side color, boolean isKing, String textName){
        thiscolor = color; this.isKing = isKing; this.textName = textName;
    }
    
}
```



Symbolic name to provide documentation to what kind of values this object have, rather than using integers.



**Import static vs non-static**

Import without static, suppose to only import things associated with a particular object

Import with static, import things that does not associated with an object



### Threads

A **thread** (thread of control) of a sequence of instructions.

Java supports programs containing multiple threads, run concurrently.

**Trick:** Logically independent of programs.

If you have two threads accessing two data objects, things can get chaotic.

We can allow a thread to lock an object. Other threads cannot use it until unlocked. Get other threads to wait.



Type `Thread`, contains information about, and controls, one thread.



Java runtime system always have threads, for example GUI, mouseClick, garbage collector.

Sometimes, we do want a real multi-processor.



It is sometimes convenient to divide events into separate sub-programs. For example, listen for requests on web server.



**Threads in Java**

`Thread chomp = new Thread(new Chewer1());`

`Thread clomp = new Thread(new walker1())`;

Call `start()` on these `Thread` objects.



Or otherwise, create classes `extends Thread`, and then can `start` on them. Define static type as `Thread`.



**Cross-Thread avoiding interference**

Undefined fashion if accessing and modifying same data.

Two edits of LinkedList on threads, second one wins.

We can use `synchronized` to decorate methods. Please wait until this object is unlocked, once it is unlocked, and let me lock it and do things with it. Then, I can unlock it again.



**Communication**

The faster party must wait for the slower.



Mark `transient` for objects in threads as other threads could have changed and you come back to it. 



`wait` method (defined in Type Object) on Object makes thread wait until notified, unlocking the object while it waits.

Check the queue.



Rather than calling each other, they send messages to each other. This will have less errors then the above methods

Check mailbox while executing.

