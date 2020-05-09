# Lec 32 Git Internals

**Version control system**: maintain a coordinated set of files by versions and many manipulations you can perform on.

Unix philosophy: lots of little tools and utilities you can scribble together and configure; little modules you can connect easily.

Git has both high-level ("porcelain", e.g. commit, convenient user interface) and low-level ("plumbing", looking at individual objects) commands. 



### Conceptual Structure

Main internal `Git` components consist of 4 types of object

* `Blobs`: hold contents of files
* `Trees`: directory structures of files
* `Commits`: contain references to trees and addition information (committer, date, log message); a graph kind of structure; collection of file versions.
* `Tags`: references to commits or other objects, with additional information, intended to identify releases or other important versions. Kind of "named" pointers.


Sometimes the data structures are shared among Trees and Commits. Persistent blobs or subdirectories.

This is a graph structure.



### Version Histories

A distributed version control system.

Commits are immutable.

Commits with multiple parent pointers: result of merging previous commits


You want commits to have unique identification across whole universe.

You can communicate these commits from one place to another.



Transmit from repo A and repo B. Anything I have already don't get transmitted. 

Repo can keep named pointers to the commits for easy access, these names are local to repo. 

Tags are also another type of pointers. 

Single unannotated tags is just a kind of branch by another name.



Commits are universal among repositories. 
There are local or cached copies of them. Git ensures the commits across places are the same.

Repository are collections of commits with some extra data.



### Internals

`.git` git repo is contained in a directory

Repo could be bare or as part of a working directory

Git internally compress info, record changes to save space than copying.

It does reorganizing or compressing from time to time.



### Pointer Problem

The need for unique way to referring to one thing on everybody's repository.

Counter that does not work.

Use the **content-addressable file system**! An object is uniquely identifiable by its content.

The idea behind Git.

If an object doesn't change, its content won't change, then its name won't change.

**Hash the content** into a much shorter String, and use that as name.

Edge case: two different content has same hash, but we pretend the hash code works!

Use a hash function that is so unlikely to have a collision that we can ignore that possibility.



### Cryptographic Hash Functions `f`

Very hard to get collision.

* Pre-image resistance: given h = f(m), hard to find m
* Second pre-image resistance: given m1, infeasible to find another m2, that f(m1) = f(m2)
* Collision resistance: hard to find *any* two different messages that f(m1) = f(m2); can you find me any pair that breaks this? No restriction of choice.

We use hash codes as unique identifiers for our Blobs, Trees, and Commits.

Highly unlikely to fail.

Is used to identifying anything from a huge collection of documents.



The entire content of the file is used for the hash.

For commit, we hash the **hashed** values of the tree contained.



Git uses `SHA1` (secure hash functions 1) produces 160 bit hexadecimal hash code.

Git uses this as a pointer to objects.

`SHA1` is not as strong as other modern ones, but sufficient for version control purposes.



**highly recommend look at `.git` directory**

There are names of files that look like SHA-1 hash code contain objects that have this hash code.



`HEAD` contains local name within repo of the current branch

`master`: the commit name that is the commit looking at currently, tip of the master branch

`objects`: interesting directory structures; a shallow tree. Directory that contains all these objects. Divided all of the commits by the first two digits. Put commits into bucket, one directory per bucket. This technique speeds things up.

`index`: contains all of the information about what file I have in my working directory. What file have I marked to add or to remove from the next commit. Contains file in my working directory. Contains contents of file I would like to commit, add, rename, etc.. In binary format, this makes it nicely to compress.

`packed-refs`: Index of collections of objects that are packed together. To save space.



### Most Interesting Ideas of Git

* Using content of file, hashed, as name of file object so it could be identified.
* Requested contents from remote based on hash codes.
* Building a system out of many tiny self-contained modules, reflected as git commands. Using them together to get the effect you want.
  * What is the hash code of a file object?
  * Given SHA-1 UID, return the type.
  * 