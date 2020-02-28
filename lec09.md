# Lec 09 Interfaces and Abstract Classes

The instance method is selected purely on the dynamic type of the value.

The only relevant thing is the type of value currently contained.

For **Instance methods (only)**, select method based on **Dynamic type**



### Fields or static methods

Static type does matter here.

Depends upon the **static type** of variable

Not a good practice for parent and child have the same name for fields or static methods 



Fields **hide** inherited fields of the same name;

Static methods **hide** methods of the same signature

Hiding causes confusion, understand it, don't do it.



Child static variable **hides** the parent static variable. (as it is more local)

Instance methods (use override)



Compiler information

`Child tom = new Child()` only knows that tom's dynamic type is a subtype of Child.

Compiler acts conservatively 

   

A kind of `generic` method

All subclasses will have at least the methods listed by the superclass.

When we write methods that operate on the superclass, they will automatically work for all subclasses with no extra work.

Anything you write that would make sense to compiler also work for members of the subclasses.



Subtypes may have more methods than superclass.



`Field`: instance variable or class variable



### Abstract Methods and Classes

Instance method can be **abstract**, No body given, must be supplied subtypes.

Can instantiate the abstract class.

But we can write methods that operate on abstract classes. 



We can make **concrete subclasses** by overriding.

`Drawable[] things = {new Rectangle(3,4), new Oval(2,2)}`



Every method should be commented, what it does, what it returns, what arguments it take

Comment on abstract superclass methods. Do not need to repeat that in subclass overriding.

`@Override` annotation

Compiler will complain if there is no such class that it is overriding or parameters are wrong.



Overriding happens at execution time. (method choosing mechanism). You can argue methods between super class and subclass are linked/related in some ways.

Hiding happens at compilation time. Fields have no relationship to each other between super class and sub class.



### Interfaces

Description of point of contact between two systems (client class and implementer class)

Specialization of abstract classes.



Interface is automatic public.

Automatically abstract.



You do not extend `interfaces`.  You `implements` interface.

Can use the interface as for abstract classes.



You can extend **one** class, but **implement** any number of interfaces. 

 

Do not put two same name constant constants in interfaces as they may clash. 



#### Higher Order Functions

Java technically that actually have higher-order functions.

Define interface stands for a function that has a simply method `apply` that does function call.

We override `apply`.

Get function without explicitly introducing a function type.

#### Lambda Expression

**Anonymous classes** 	

```java
R = map (new IntUnaryFunction(){
    public int apply (int x) {return Math.abs(x);}
}, some list);
```

equivalent to 

```java
class Anonymous implements IntUnaryFunction{
    public int apply(int x) {return Math.abs(x);}
}
R = map (new Anonymous(), some list);
```

Even more suficient

```java
R = map ((int x) -> Map.abs(x), some list);
```

