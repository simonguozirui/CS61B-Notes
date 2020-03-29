# Lec 22 Game tree

### Generate and Test

Instead of taking an entire of set of possibilities and going through them, we generate elements on the fly to find what we want.

### Backtracking Search

When you are stuck, you back up and try something else.

From current position, try possible moves, if all of them failed and I cannot continue with any of them to the end, then I report failure. Whoever called me, try the next move.

Recursive nature.

 

**Search for the Best Move**

How do we know what is good? Heuristic value (guesses).

Static evaluate the board situation, number of pieces, weighted sum of values, nearness of pieces to strategic areas.

This is static, how can we go ahead? Look several moves in the future

How things are going to look in several moves given we make a particular move now.

What you do, what your opponent is going to do, what then you do, etc..



### Game Trees

Think about this problem as a tree. A conceptual tree.

Nodes are positions, edges are moves.

**Minimaxing algorithm**: Maximum of next moves, which are the minimum (caused by opponents) of the moves after that.

Value associated with the eventual position chosen as the value of my current play



### Alpha-Beta Pruning

Pruning the tree as we go so we don't have to look at certain things

Stop if no point looking any further, and prune (not process) a branch.

Each parent sends down to the children, the range of values that it knows that is going to be acceptable

Anything outside of this range, I am not interested in.

The child, the search for a move, use that information to discontinue search upon finding out any further work is futile.

Amount that we save continues to grow as tree gets bigger

branching factor, effective arity of these nodes, allow us to look further than we have to look



When to stop?

If you can hit the bottom of the tree, you can force a win.



However, you cannot go very deeply.

Sometimes, you are within a forced win despite your opponent's best effort. But doesn't happen often.



Choose a maximum **depth**. Instead of going further, we will just use the static evaluation if we are at the maximum depth.

For project 2, having more pieces is not necessarily a good thing. Turns out it is advantageous to have just a single piece while your enemy has lots of pieces. A single piece is in one connected group. But having more pieces give your moves and possibilities.



**Iterative deepening** repeat the search at increasing depths until time is up. Go down one level at a time until time is used up.



Or you reach a sequence of captures.





### Algorithm

A tree-motivated search.
We don't have a data structure, we are generating moves on the fly. 

Same structure as exploring the tree, instead we don't have a tree this time.



Search will be exhaustive down to a particular depth in the game tree; below that, we guess values.

Also pass alpha and beta limits:

- High player does not care about exploring a position further once he knows its value is larger than what the minimizing player knows he can get (beta), because the minimizing player will never allow that position to come about
- Likewise, minimizing player won't explore a positions whose value is less than what the maximizing player knows he can get (alpha)

![Alpha-Beta Pruning](C:\Users\simon\OneDrive\Desktop\CS61B\Notes\alpha-beta-pruning.PNG)



`simpleFindMax` update alpha, use heuristic value, look at the possible next position, static evaluation

`simpleFindMin` update beta, use heuristic value, look at the possible next position, static evaluation

**Find Max**

`findMax` call `findMin` (values from subsequent moves); 

a maximizing player will find a move with `findMax(current position, search depth, -inf, +inf)` to start with

Subsequently, it will call `findMax(next, depth-1, alpha, beta)`

**Find Min**

`findMin` call `findMax` (values from subsequent moves); a minimizing player will find a move with `findMin(current position, search depth, -inf, +inf)` to start with

Subsequently, it will call `findMin(next, depth-1, alpha, beta)`



These two functions alternatively call each other until depth is exhausted, then we use a heuristic evolution.



If alpha and beta cross, there is no point in going any further. We exceeded the value that the other player is going to accept.