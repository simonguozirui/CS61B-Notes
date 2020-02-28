# Lec 08 Object-oriented Mechanisms

In a real instance method, as a convenient abbreviation, one can leave off the leading "this." on field access or method call if not ambiguous

**Instance and static methods don't mix**

static methods have no implicit `this` parameter.

 Error message "attempt to access instance method from static context"



You can reference static fields inside static methods or instance methods.



Constructor is kind of special instance method that is called by the **new** operator right after it creates a new object.



All classes have constructors . 

In the absence of any explicit constructor, get **default constructor**. 

Multiple **overloaded constructors** possible. They can use each other.

`this(head, null)` call another constructor with the arguments`head` and `null`. Must always be at the beginning of   your constructor.

Instance variables initializations are moved inside constructors that don's start with this(..). Copy that value. 






#### Object-Oriented Mechanisms

**Writing software that operates on many kinds of data.**

Demodulating things.



Problem 1

Java is a statically typed language. How can we use `print(x)` regardless of type of x?

We can use overload methods. 

Java, C++ supports overloading. Complier will sort things out and choose which one to execute.



Problem 2

How to get a list of anything or array of anything?

In Java, lists and arrays have a single type of data.

Any **reference** value can be assigned/converted to type `java.lang.Object` and back, so can use Object as the "generic (reference) type"

```
Object[] things = new Object[2];
things[0] = new Intlist(3, null);
things[1] = "stuff";
((IntList) things[0]).head == 3;
```



The primitive type of values are not really convertible to Object.

A set of **wrapper types**, one for each primitive type.

byte --> Byte

long --> Long

float --> Float

short --> Short

char --> Character

double --> Double

int --> Integer

boolean --> Boolean

`Integer Three = new Integer(3)`

`int three = Three.intValue();`

**Autoboxing**. In situation that you are interchanging primitive wrapper types with primitive type, things will work out correctly.



### Dynamic vs Static Types

Every **value** has a type -- it's **dynamic type.**

Every **container** (variable, component, parameter), literal, function call, and operator expression has a a type -- it is **static type**. All known to the compiler already.

Therefore,  **every** **expression** has a static type.

Sometimes static type and dynamic type don't agree with each other.



##### Type Hierarchies

Container with static type T may contain a certain value only if that "is a" T -- that is, if **the (dynamic) type of the value is a subtype of T.** 

A function return type T may return only values that are subtypes of T.

All types are subtypes of themselves. (reflexive)

Reference types forma type hierarchy. Some are subtypes of others.

All reference types are subtypes of `Object`



Java Library Type Hierarchy (Partial)

Java is designed so that **any expression of (static) type T always yields a value that "is a" T.**



Static types are "known to the compiler", because you declare them or declared by the Java language.



L = E

(Right) E's static type must be a subtype of (Left) L's static type.

The dynamic type (value) of E must be a subtype of E's static type, and hence a subtype of the static type of L.

Similar rule apply to assignment, E[i], parameter.

Subtypes are transients. X is subtype of Y. Y is subtype of Z. X is subtype of Z.

Assignment, passing into parameter, assign to array, these cases rules all apply.



When you deal with primitive things , certain primitive types might be **coerced** from one to another.

`short` can be **coerced** (converted) to a value of type `int`

`short x = 3002;` works fine.



#### Consequences of Compiler's "Sanity checks"

a **conservative** type



The casts ((int[]) x ) just informs the compiler of the type, don't change stuff

`Static type of cast (T) E is T`



You can over ride definition!



Conveniently, the "+" operator on String calls `.toString` when asked to append an object, conveniently converts.



`class B extends A{}` class B is a subclass of A

All the fields in A is also inherited by B. This is the object-oriented part.

B is allowed to override instance methods of A.



**For Instance methods (only), elect method based on dynamic type.**

`X.f` get the particular version of f that applies to the dynamic type of X.



Simple to state, but we'll see it has profound consequences.





 

