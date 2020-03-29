# Lec 25 Generics

 Since Java 1.5, Java introduced parameterized types like `List<String>`

### Parameterization

Can think of them as functions that take a type as a parameter.

`public class ArrayList<Item> implements List<Item>` introduced formal type parameter, whose "values" (which are reference types) get substituted for all the other occurrences of `Item`  when `ArrayList` is called.

Other occurrences of `Item` are uses of the formal types, just like a formal parameter in the body of a function.

Substitute type as value



### Instantiation

Give it an actual type `ArrayList<String>`. In effect, you get a new class and new interface `List<String>`. All of the occurrences of Item get replaced by `String`.



### Generic Functions

Functions (methods) maybe also be parameterized by type.

`static <T> List<T> singleton(T item) {..}`

`static <T> List<T> emptyList() {...}`

**Type inference**

* The compiler figures out T in the expression of singleton(x) by looking at the type of x
* `List<String> empty = Collections.emptyList()` compiler deduces parameter T from context as it must be assignable to `String`.



### WildCards

Wildcard type parameters say that you don't care what a type parameter is (it could be any subtype of `Object`)

`static int frequenc(Collection<?> c, Object x)` instead of

`static <T> int frequency(Collection<T> c, Object x)`



### Subtyping

How can you compare generic types?

<- subtype

If `List<String>` <-/is a subtype of `List<Object>`, this would violate type safety. The compiler is wrong about the type of a value.

For `T1<x>` <- `T2<y>` , they must have X = Y

For `T1<x>` <- `T2<x>` , then T1 <- T2 The first base type must be a subtype of the second base type **and** parameters have to be identical.

 Same parameter and return types for the methods. Same method signature.

Due to inheritance, the methods of the parent type is a subset of the child's type.



In Java, there is an exception. `String[] <- Object[]` even they have different type parameters.

Compiler would ignore this though (maybe issue warning), but it will cause `ArrayStoreExcpetion` a runtime error while executing dynamic types if you stored the wrong type of value.

This inconsistency is created to allow things like `ArrayList` to be implemented.



### Type Bounds

Specifying the type of the parameter, restricted.

`class NumericSet<T extends Number> extends HashSet<T>`

ensure a parituclar type parameter is replaced only by a subtype (or super type) of a particular type.

because compiler cannot guarantee that T has comparison operation methods.



Python duck-typing: if it walks like a duck, quacks like a duck, it is a duck. Python has no type specified and figure it all during runtime.



`static <T> void fill(List<? super T> L, T x)` set all elements of L to X.

L can be List<Q> for any Q where T is a subtype of Q through extends or implements.

e.g. A List of Objects filled with String



`static <T> int binarySearch(List <? extends Comparable<? super T>> L, T key)`



Behind the scene, Java creates raw type and type casts them. For example, just Foo() or List().

e.g. Translate `List<String>` , `List<Integer>` into plain `List`. Info that they are different is lost.

 Java does this to ensure backward compatibility. Compiler check type is correct. Casts to check type.

Occasionally, it cannot guarantee all that all the cast will work and compiler will give `unsafe` constructs warning.



### Limitations

You cannot `instanceOf` to distinguish before `List<String>` and `List<Integer>` 

All kinds of Foo class or List class are really the same type at runtime, you cannot distinguish them. That type information is lost at run time. You cannot ask these questions.

Not a big deal, because we are not suppose to use `instanceOf` for OOP designs a lot.

Inside the raw class, you cannot write new T(), new T[]. or x if `instanceOf` T as compiler needs to know explicitly what type T is.

new T[] is okay because you can do new Object[]

new T() more problematic unless using Factory methods to produce new objects instead of constructors.



Primitive types are not allowed as type parameters `ArrayList<int>` not valid. 

Automatic boxing and unboxing handles this. However, boxing and unboxing have significant costs.

 