# Lec 14 Integers

Downcast from parent to subtype even at compile time we don't know that but we will check in run time

Downcast to let protected fields being accessed. As long as static type is subtype or child of extended class.

Without casting, the compiler is concerned about the case of an unrelated subtype.

But if it is unrelated subtype, it might occur in runtime to fail. 

Compiler being conservative, saying this might fail, we should make this illegal. Give us a compile time error.



`this`'s static type is defined in the class of where it is right now.



### Access Control cares about static type only 

`public` and `private` do not apply to dynamic types. 

It is possible to call methods in objects of types you can't name.



The default access is package private.



### Importing

You can write it `java.lang.regex.Pattern` every time but you can shorten that by importing.

`List` can be used as an abbreviation for `java.util.List` after importing that. 

`java.util.*` style guide don't like that. Put some documentation on what other classes and packages that you are depending on. Write things out.



Purely an abbreviation thing (plus some documentation). No special access provided.

Java automatically always contains `import java.lang.*`



**static importing**

static members. Abbreviate such references.

`import static java.lang.System.out` you can just use `out` now.

Useful for `Math` package.

You cannot do it for anonymous package. You have to have a package name for import.



### Nested Classes

Sometimes it make sense as two classes are closely related 

* be used only in the implementation of the other
* be conceptually subservient to the other
* avoid namespace pollution

**Static class**

```java
class Polynomial{
    // Methods on polynomials. 
    private Term[] terms;
    private static class Terms{..}
    // static that are just oridnary classes but nested defined in some other class
    // can be accessed as Polynomial.Terms if access control allows such operation.
}
```

 

**Inner class**

non-static class. 

Provides an linking.

Each instance of the nested class is created and naturally associated with an instance of the containing class.

```java
class bank{
    public class Account{
        Bank.this.xxx(..);
        //Bank.this means the bank that created me
    }
}

Bank e = new Bank();
Bank.Account p0 = e.new Account(..); 
//which bank am i creating under
```



### instanceof

`r instanceof TrReader`

true if dynamic type of R is a subtype of `TrReader`

Use instance method rather than a lot of if statements with `instaceof`

Virtual methods instead of if statements



### Integers

Five types

byte, short, char, int, long

Unicode standards.

`N bits` means there are 2^N integers in the domain of the type.

If signed, range from -2^(N-1) to 2^(N-1)-1

If unsigned, range from 0 to 2^N-1, non-negative numbers

### Overflow

What if arithmetic overflows?

You get exact a value mathematical answers but modular to "wrap around"

Clock arithmetic. The next number after the largest in an integer type is the smallest

(byte 127+1) == byte(-128) as byte ranges from -128 to 127

If the result of some arithmetic subexpression is supposed to have type T, an n-bit integer type

Then we compute the real mathematical value, x

and yield a number, x', that is in the range of T, and that is equivalent to x modulo 2^n  

(x - x') is a multiple of 2^n



This modular is different than % as it treats differently for negative values



Modular rules, helpful to note down.

