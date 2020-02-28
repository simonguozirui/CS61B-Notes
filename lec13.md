# Lec 13 Packages, Access, Loose Ends

Exceptions help communicate erros

Exceptions are objects that can carry info. They have subtypes `Throwable`.  There are some more subtypes `Error`, `RuntimeException`, `Exception` (for anything else).

Two types of exceptions

1. Pre-declared exceptions are all subtypes of one of those. Any subtype of Error or RuntimeException is said to be **unchecked**. Your exceptions should be `RuntimeException`.

   Don't need a documentation. 

   Programmer errors: IllegalArgumentException

   Errors detected by the basic Java system (NullPointer, OutOfBounds, TypeCasting)

   Could throw anywhere or anytime. 

2. All other exception types are checked. 

   Circumstances that don't necessarily is a programmer example.

   Attemptin to open a file that does not exist. 

   Input or output errors on a file. 

   Receiving an interrupt.

   Every checked exception that can occur inside a method must either be handled by a try statement, or reported in the method's declaration, Give persmission for body of method to throw exception,`void myRead() throws IOException, InterruptedException {...}`. Throws just to mean "I might throw"

   Static parent, dynamic children. You don't know when the child points are when you compile things. So you cannot `throw` errors on child's overwritten method if parent's method does not have Excpetions. (Compile time error)

   You should get child and parent both have exception, or just parent if the child never throws an exception if it will never go wrong.

   If you might throw exception, you should indicate it in `throws` in method declaration.

   It is perfectably okay to put unchecked exceptions in throws although useless.



### Good Practice

Throw exceptions generally better than print statements.

Sometimes the program is totally ready to deal with exceptions.

Nice to throw exception when programmer **violates preconditions**. For example, IllegalArgumentException for libraries.

Assert things to make sure things are right at the right part of the programmer. 

Throw them better than letting wrong values pass through.



You can attach abritary info to expcetion, by making extention of the `Exception` class.



### Package Mechanics

Clasess correspond to things being modeled (represente) in one's program.

Packages collected classes, interfaces, and other packages.

Putting everything together, avoid name crashing. 

Group them in logical fashion. Separate concerns.

**Anaymous package** end user classes, one-off.  By default, a class resides there.

Organize class path. Package as directory organizaton.

`jar` ( Java archive) file is a whole bunch of directory tree compressed into a single file.



### Access Modifiers

Purpose is to allow the programmers to indicate intended uses/audiences .

`private`, `public`, `protected`

There are certain things that you need to know and rather you not know.

Keep them separate, and access modifier is an enhanced documentation.

Security concerns



**Accessibilty always determined by static types**

The true thing that compiler knows about.

How the member's decrlartion is qualifeid and where it is being accessed



`public` avliable everywhere from any package. Represent specifications.

`private` avalibel only within the text of the same class, **even for subtypes. **Conceal implementation.

`package private` (defaulted) available only within the same package.  For internal implementations. Always care about which package we are in. 

`protected` members of C1 are avalibale within P1 as for package private. **Outside P1**, they are avliable within subtypes of C1 such as C2 (`C2 extends C1`), but only if accessed from expressions whose static types are subtypes of C2.   Extendable classes that extention could be used. 



May override method only with one that has at least as permissive an access level. Avoid inconsisency among methods that are overwritten.







