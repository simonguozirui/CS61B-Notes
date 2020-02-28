# Lec 05 Arrays

**Former program verifications**

How to go about writing loops?

What does the loop body do each time through?
What is true every time. (invariant)

You don't trace the loop through every iteration.

You can characterize through typical iteration.



### Arrays

a particular kind of structural container

Length, a fixed integer

A sequence of $length simple containers of same type, numbered from 0

Arrays are anonymous, like other structured containers

Arrays referred to with pointers

`A.length`

`A[i] `(0 through length but not including length)



`int [] x;`Empty array variable declaration. Make sure `null` is not arbitrary and does not let you use it anyway.

`variable not assigned before use` compile time error



```java
int[] x;
System.out.println(x); //this would error in compile time
x = new int[3];
System.out.println(x[0]); //this is perfectly fine, prints 0. 
```



New syntax

```
for (int x: A)
	N+=x; 
```

Sometimes to loop backwards is helpful.

```java
import static java.lang.System.arraycopy;

System.arraycopy(arr, k, arr, k+1, arr.length-k-1);
// from, to, # of elements to copy
```



 Space and time inefficiency, turn it into tail recursive

