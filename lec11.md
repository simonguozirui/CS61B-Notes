# Lec 11 Examples: Comparable and Reader

Elegance over speed nowadays as computer get more powerful.

With an interface, we already can write program that use this interface even before we implement it.

  

Power of separation of concerns (from the client, according to the spec, the implementer, accord to the spec)



Compute lazily until a method is called. Regenerate data each time.

Information withheld from the client, it is a good thing.



The amount of info that the client need to know to use this is diminished and therefore the complexity of using it is smaller.



With one interface, many different implementations.

Dynamic dispatching and inheritance to figure out what needs to be done at each particular case.



### Comparable

Separate interface. Things are compared are Objects.

Have one method `int compareTo(Object obj)`

returns `int`. If this is less than that, return less than 0.

If it is more than, returns more than 0.



You can use a general-purpose max function.



compare some type of object to another type, will throw exception



cast for `Object obj` to get exception

`IntSequence x = (IntSequence) obj`



If class does not have `Comparable`, put a class that extends it and implement `Comparable` if the class already have a method `CompareTo` (without `@Override`)

Adding interface later in an extension



Conform your type to some interface that was not around back when you created it.

```java
public interface Comparable<T>{
	int compareTo(T x);
}
```

No need to cast now. 

`class IntSequences implemetns Comparable<IntSequence>`

No need to cast, all types are known.



`<T>` is like a formal parameter for interfaces, and they are types not values.



### Readers

`java.io.Reader`

`int read()` positive values represent characters, negative represent end of stream. Use `int` than `char` give extra information.



Abstract class with implementation can be useful for **partial implementation**, the template class pattern

