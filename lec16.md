# Lec 16 Complexity

Cost means 

* Operation cost (time, space)
* Development costs
* Maintenance costs
* Costs of failure

Overengineering is not optimal.



Is it fast enough? For what purpose, for what input data?

How much space (memory, disk space)? Depends on what input data.

How will it scale? as input gets big?



UNIX philosophy, lots of utilities do something focused on one area. OS (shell) glue them together.



Simple scripting

Correct engineering principle: keep it simple (do not do unnecessary optimization)




### Cost Measures (Time)

**Wall-clock or execution time**

`time java FindPrimes 1000` get timing figured out

Applies only to specific data set, compiler, machine, etc.

Does not answer the general question of how fast is this program.

**Dynamic statement counts**

Count the number of times statements are executed

More general, not sensitive to speed of machine.

Does not tell you the actual time, and only applies to a specific data sets that I run it on.

**Symbolic execution times**

Formulas for execution times as functions of input size.

Applies to all inputs by definition. Make scaling clear.

Practical formula is going to be approximate, so we know very little about actual time.

Roughly proportional to exact time.



### Asymptotic Cost

Engineering principle: If you are going to be approximate, you do not need to be precise.

Asymptotic, what speed do we approach when input get bigger than bigger

Doesn't matter

* On fast in run on small's inputs. as small cases can be pre-calculated. We are more interested in asymptotic behavior as input size becomes very large.
* Constant factors is not a big concern. We are interested in the shape of the costs

How can we abstract away from these details when it is important?



### Order Notation

A general notation, behavior and size of function.

Families of function that have similar behavior. "f is bounded by g if it is in g's family"

* g(x), 2g(x), kg(x) behaves the same way g(x) does, same family as g(x)
* h(x) = K*g(x) for x > M has g's shape "except for small values", the ignoring small input principle, same family as g(x)

We use that family as upper or lower limits.

Upper limit O(g): throw in all functions whose absolute value is everywhere <= some member of g's family.

Lower limit Ω(g): throw in all functions whose absolute value is everywhere >= some member of g's family.

Θ(g) = O(g) ∩ Ω(g), the set of functions bracketed in magnitude by two members of g's family.



f bounded by multiples of g.


notation convention`f(x) ∈ O(g(x))`



**Cost functions (what we are interested in)**: functions that measure the amount of execution time or the amount of space required by a program or algoirhtm.s



Why scaling matters?

Constants get swamped by order of growth.



How much data (problem size N) can I process in a given time? 



The big O bound is loose.

We are saying things about the largest possible time required. 

To so as much as possible about our worst-case time, put a Θ bound as we know how much it at least take and how much at le.

None of this tell us what happens in the best case



Use N > M provision (in definition of O(N)) to ignore empty list case.