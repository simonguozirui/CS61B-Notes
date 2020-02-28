# Lec 03 Values and Containers

Have a picture of the program in your mind
Think about the model.
Build it in code.

### Values
numbers, booleans, and pointers are considered values
Values never change

### Simple containers
Things that hold values. Can hold different ones over time.
varibales, fields, individual array elements, parametsr
Container holds certain type of value. Only accept values that thea type they are declared as.

### Structured containers
Contain (0 or more) other containers.
Class object, array object, empty object

Pointers are values that point to structured containers
Think about arrows as addresses

Structed containers hold simple containers that can point to more structured containers


In Java, assignment copies **value** from one simple container to another.

Copy pointer. 


### Arrays
Fixed length

`IntList` is a recursive data structure.
```
public class IntList{
    public int head;
    public IntList tail;

    // constructor
    public IntList(head, tail){
        this.head = head;
        this.tail = tail;
    }
}

```

### Simple classes
All code has to live in a class

### Destructive vs Non-destructive operations
Destructive vs Non-desctructive
`desctructive` modify the input objects

`non-desctructive` leaves the input objects
It is okay if it is point to the same thing, 
but if you need to change the value but you better create a new object.

Create new object, use `new` keyword

Recursive definition
```
static IntList incrListRecursive(IntList p, int n){
    if (p == null) {
        return null;
    } else{
        return IntList(p.head + n, incrListRecursive(p.tail, n))
    }
}
```

Usually if you have an recursive data structure, use it as a base case.
Don't do arm-length recursion. `p.tail == null` Avoid repeat computation from recursive case in base case.

Easier to use recusion for recursive data strucutre than using iterative approach.


### Models of memory