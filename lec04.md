# Lec 04 Simple Pointer Manipulation

Keep track of the list that we are returning and the last element that we are tracking

`final` keyword, this variable may not be changed after the variable is initialized
This method will never been overwritten.

Destructive solutions may modify objects in the original list to save time or space.

Recursion.
Looks like start to front
When you trace it, it builds it from the end

`continue` jump down the loop, skip/go down to the end, start the next iteration


`last = last.tail = new IntList(last.head, null)`
Goes backwards
Assign `new IntList(last.head, null)` to `last.tail`, then assign `last.tail` to `last`

Loop invariant
Come up with a body that advances your calls forward
What I am assuming that make that loop work?

`invarient` condition that is the same each time
