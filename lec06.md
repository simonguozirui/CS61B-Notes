# Lec 06 Developing a Sort, Unit Testing



Previous lecture

Iterative solution

Note the **Invariant** parts

Draw pictures in mind, to see what in mind what is still true, what are you keeping.



### Multidimensional Arrays

Build them as arrays of arrays

```java
//method 1
int[][] A = new int[3][];
A[0] = new int[] {2,3,4,5};

//method 2
int[][] A;
A = new int[][]{{2,3,4,5},{4,9,16,25},{8, 27, 64, 125}};
//method 3
int[][] A = {{2,3,4,5},{4,9,16,25},{8, 27, 64, 125}};
//method 4
int[][] A = new A[3][4];
for (int i = 0; i< 3; i++){
    for (int j = 0; j<4; j+=1){
        A[i][j] = (int)Math.pow(j+2,i+1);
    }
}
```

An array of rows, each element of A is itself an `int[]`, a row



`Math.pow` returns Type Double



You can have un-rectangular arrays of arrays. 

Because length of the array is not part of the type, contrary to C.



```java
ZERO[0] = ZERO[1] = ZERO[2] = new int[] {0,0,0};
//they all point to the same array
```



Elements of an array whose values are references are null by default.



### Sort an Array

Takes elements on command line in lexicographic order

```
public class Sort{
	public static void main(String[ words){
	
		sort(words, 0, words.length-1);
		print(words);
	}
	//Sort items A[L..U] with all others unchanged
	static void sort(String[] A, int L, int U){
		// to be completed
	}
	//Print A on one line, separated by blanks
	static void print(string[] A){
		// to be completed
	}
}
```



### Testing

**Unit testing** refers to the testing of individual units (methods, classes) within a program, rather than the whole program.

JUnit tool for unit testing.

**Integration Testing** refers to the testing of entire (integrated) set of modules, the whole program

**Regression Testing** refers to testing with the specific goal of checking that fixes, enhancements, or other changes have not introduced faults (regressions). Make sure you don't go backwards. You don't do something you undo with that part fix.



### Test-Driven Development

Idea: write tests first.

Implement unit at a time, run tests, fix and refactor until it works

##### Testing sort

Give a bunch of arrays and make sure they each get sorted properly

**Corner cases**: Empty array, one-element, all elements are the same

**Representative "middle" cases**: elements reversed, elements in order, one pair of elements reversed, ...





#### JUnit

Handy tools for unit testing

Annotation `@Test` on a method tells the Junit machinery to call that method

An **annotation** in Java provides information about a method, class, etc.. that can be examined within ava itself.

A collection of methods with names beginning with `assert` then allow your test cases to check conditions and report failures.



`==` checks the value of the things you are comparing

When you compare two pointers, it is only equal if they are pointing to the same address. `assertEquals`

We want to check contents of arrays, we can use `assertArrayEquals`



### Selection Sorts

Goal: Sort items A[L..U] with all others unchanged

Find the largest Index s.t. A[k] is largest in A[L], ..., A[U]

Swap A[k] with A[U]

Sort items   L to U-1 to A by recursively calling the function.



Note: swapping variables in Java you cannot assign two of them to each other in one line. You need to have a temporary variable.



Recursive structure to iterative structure

You change the iterative parameter