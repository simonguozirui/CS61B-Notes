# Lec 12 Additional OOP Details, Exceptions

`java.io.Reader` abstracts sources of characters

Result still abstract: can't use `new` on it.

I can have the `Reader` interface before implementing anything



`wc` method Using abstract method `read` can work on any `Reader`



Client --> Interface  --> Concrete class --> Implemented from an Abstract Template



`Reader` interface class served as a `specification` for a whole set of readers.

Ideally, most client methods that deal with `Reader`, like `wc`, will specify type `Reader` for the formal parameter, not a specific kind of `Reader`, thus assuming as little as possible.

And only when a client creates a **new** `Reader` will it get specific about what subtype of `Reader` it needs.

Client's methods are as `widely applicable` as possible.

`AbstractReader` is a tool for implementers of  non-abstract `Reader` classes, and not used by clients.

`Comparable` interface allows definition of functions that depend only on a limited subset of the properties methods) of their arguments (such as "must have a `compareTo` method")



**Dynamic Methods** are quite nice.;



Finish Java related materials.

`Inheritance`, `dynamic concepts` are general CS concepts.

Write more general problem. Ad-hoc --> institutional



Separate the concerns of implementers and the client

Implementers need to keep things away from clients, need to keep complete control.

Control initialization of the objects.



Java has rules to make sure constructors is safely called when new object is created.



When a class extends another, there are 2 constructor (1 for the parent class/constructor and 1 for the child class.)

Java **guarantees** that one of the Parent's constructor is called first.

```java
class Recntangle extends Figure{
    public Rectangle(){
        super(4); //call parent constructor
        // or you call another consturctor in the same clas by this.xxx
        // But that eventullly calls parent constructor
    }
}
```



**Java does automatic things for you**

Java calls the "default" (**parameter less**)  constructor if there is no explicit constructor called.


If you don't have any constructor in your class, Java will provide one for you.



Be careful about default constructor as it pass no parameters for `super()` and thus if parent class constructor needs any parameter it will error in compile time.



If either I do it explicitly in the first line, or Java does it for me.



As long as I call parent constructor correctly, I will be fine, even my child constructor has different param than parent constructor.

Anytime you create an object, you call all the way to the `Object`'s constructor.



### Using an Overridden Method

`super.cogitate(x,y)` Calls overridden function

You cannot call grandparent's method that is overridden. Parent don't allow talking to grandparent.

 

### Trick: Delegation and Wrappers

Monitor is a **wrapper class**

`Monitor(Storage x)` it saves x

Used the save x to do actions, and keep track using class variable.



## What to do about errors?

Errors: 

1. External (bad input, network failures)
2. Internal errors in programs

Large amount of any production program devoted to detecting and responding to errors.

In Java, we **throw exception objects**

`throw new SomeExcpetion (Some description)`

`throw` causes each active method call to `terminate abruptly`

Catch exceptions and do something corrective with try.

To avoid that, use `try`

```java
try{
    Stuff that might throw exception
} catch (SomeException e){
    Do something reasonable
} catch (SomeOtherException e){
    Do something else reasonable
}
Go on with life;
```

Descriptive string (if any) available as `e.getMessage()` for error messages and the like.



OOP aspects. `IOException` includes exceptions like `FileNotFoundException`, `MalformedURLException`.

Don't do `catch (Throwable ex)`, that is just lazy.

You can concatenate types of exceptions by `|` .