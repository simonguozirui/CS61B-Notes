# Lec 07 Object-Based Programming

From last time.

`indexOfLargest` 

Recursive call, take the index `k` of largest value in V[i0+1, ...i1]

Then compare the element.

This is how you **compare Strings**. as `String[] V`

`return (V[i0].compareTo(V[k]) > 0) ? i0 : k;`

same as

`if (V[i0].compareTo(V[k]) > 0) return i0; else return k;`

You are comparing the last two elements during the first call.



Use library procedure if possible to keep things simple.



`System.out.printf` allow you format your print statements.



`compareTo` compares first element and second element. 

return positive number if first is bigger

return negative number if second is bigger.



For string. return positive number that describes what character index it was to return positive or negative values.



### Object-Based Programming

How to manage large programs? 

Modularize and organize them.

Organizing units are:

**Function-based Programs** around functions (methods, etc.), data structures (objects) are considered separate).
Inputs and outputs define the program. Data structures for input and output.

**Object-based Programs** around the types of objects that are used to represent data; methods are grouped by type of object.



**data type** set of possible values or possible operations that can act on these values or things that contain these values

**Abstract data type**

- a set of possible values (a domain)
- a set of operations on those values (or their containers)

Preferred method is a **procedural interface** so you don't need to know how data is constructed. Hide all the details.

Separation of concerns.

**Class declaration** defines a new type of object.

**Instance Variable** simple containers within these objects (fields or components)

**Instance methods**  ordinary static methods that take an invisible extra parameter (this)

**Constructor**

`public Account( int balance 0)` no return type, same name as class name. Initializing.

`this` is like `self`

Special methods that are used only to initialize new instances

When you use an instance variable in method, Java will supply the `this.` for you.

Take arguments from the **new** expression.

**new** keyword, indicate creation of new instance.

**Method Selection** picks a method to call. What object (pointing) and what is the method name

`A.b` b is something instead of A



Initialize value (= something) outside of constructor is a short hand to assign to values using constructor



For instance variable, you begin with `_variable`



**Getter Methods**

Make instance variable private. Allow public access only through methods.



If I declare some variable to be `static`, it is a variable shared by all Class instances.



