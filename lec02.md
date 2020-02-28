# Lec 02 A Little Programming

Problem: print program prime numbers thru U

###### Top-down
look at the problem as a whole
Figure out some nice clean pieces which can be broken down

Recursively goes down look at these pieces.

Decomposing my problems into pieces.
Assume my pieces are implemented correctly.

###### Smaller --> Big
Smaller pieces of code that does some things and assemble them together

Write parameters in all Caps in documentations

Java's integer has range


`Guard` condition

You don't trace recursive call all the way down. You do one level down.

Lesson: Comments aid understanding. Make them count! Have faith in it.

You are forced to rely on the comment in Java programs since you cannot see how functions are actually implemented.

`Tail recursive` creates an `iterative process`

the machine that you are compiling should not drive your code

initial, test, value

Inefficient, we check values that we do not need to check.

Generally good to keep these methods to be self-contained, no hidden assumption that relies on the rest of the program.

Floating point operation are all approximations

