# Lec 10 Interfaces and Abstract Classes

Java's alternative to Python's function

1. define a class
2. pass around an object of that class
3. have the standard method that execute the function body

Have a interface to be the make this class the subtype of that interface.

Call back functions. The interface (GUI) will call back to your code.

Have an interface, a class that implements that interface, overrides that method of the interface. 

Interface type become parameter type

`java.util.function.Consumer`, which is a one-argument method

Java will figure out what type to define for argument from the context for the one line call back function. Use whatever interface that contains the right method.



### Inheriting Headers vs Method Bodies

 Multiple interface inheritance, but single body inheritance 

You can implement multiple interfaces, but extend only one  class.

**What goes into interface?**

Abstract methods and static constants, and default methods

Java 8 default method, if no subtype defines it, it will use the default method defined in the interface.

Interface is a kind of abstract class  (kind of)

  



From a static instance, there is no `this` pointer.

Restriction on static method.

It cannot use `this`. Other people can. `this.f()` the f defined in whatever class `this` have.

The compiler always decide if a certain thing is correct and what it means on the class that it is in. 

`this` within any kind of class is whatever class you are in



Reference static method, reference the one that it is in the same class as where the function is called.

The static type of `this` is the type of the surrounding class.

But the rule of how `this` works is the same as ordinary variables.

If it is a instance method, never mind the static type, just care about the dynamic type of `this`.



 Static methods select static type

Dynamic methods select dynamic type



Clients are not concerned about how it is implemented but rather what methods it provide

Clients are intended to rely on specifications

Syntactic specification (syntax that needs to use),  semantic specification (comments)

 

Without knowing the implementation, I can define and implement these methods based on the interface specification.