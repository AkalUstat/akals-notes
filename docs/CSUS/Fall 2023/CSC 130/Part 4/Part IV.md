Recursion!!!!

# I. Program Structure
To write good software, a good understanding of the behind the scenes is needed, especially in terms of memory.

## Terminology
***Arguments***: Data passed to a function when it is called.
***Parameters***: the format of the functions when it is defined (arguments follow the parameters).
arguments $\rightarrow$ (passed to) parameters 1:1.
******
***Scope***:how a variable/function is visible to the rest of the program. 

Some are *global variables*, which are visible to everything. They are useful for sharing data, but are problematic because unexpected modification can cause side effects and are not cleaned up when they are done.

A better (generally) strategy is to use *local variables*, which are only visible to the function in which they are declared. Parameters are local variables. 

# II. System Stack and the Heap
The two types of memory that computers use for programs. They grow towards each other. 

***System Stack***: grows up. Used to store local variables and allows your program to support functions, whose calls are added here as *activation records* that contain all information that the function instance requires; parameters, local variables, return address. Data from the record does not persist after the function ends.

The FILO nature of the stack allows function nesting and recursion. As they each return on the stack, the record is popped, and only the return value is passed to the caller.

***Heap***: grows down. Stores *dynamic allocation*, which means it is allocated as needed. It persists for a longer time, regardless of function calls, and is cleaned up by the GC when it is no longer needed.

# III. Reference Types

*Reference types* are ADTs. They link to nebulous objects whose contents and implementation are unknown (OOP). This means that local variables exist on the stack but reference the actual objects stored on the Heap (multiple variables can point to the same object: *aliasing*).

The system keeps track of these references and when there are no references, the GC reclaims the memory. This introduces a bug: you can remove an item from an ADT, like a list, but there still exits a link to it. It's been *orphaned* and *loiters*: still exists but cannot be accessed. 

# IV. Pools: Harnessing Loiters
We can harness loiters to optimize: Since creating and destroying objects on the heap is expensive, we can create a *pool*, a collection of nodes that are allocated early and used as a recycling bin.

![[Screenshot 2023-10-04 at 11.07.28 AM.png]]

If a node is needed, it is removed from the pool. Once its use is over, it is set to null and put back into the pool. 

However, maintain a limit on the size of the pool, otherwise it'll grow forever. 

# V. Recursion 
Break a function down into its most basic form (break it down into identical, smaller problems) until a base case is reached. A function calls itself; costly on resources.

## Danger
A proper implementation of recursion must break down into a single value (base case). If it doesn't the program won't stop recursive, resulting in a *Stack Overflow* or *Heap Exhaustion* error. 

## Ask Yourself 

1. Does the program lend itself to recursion? 
	1. can it be broken down into smaller instances?
	2. is there a better iterative implementation?
2. Is there a base case? 
	1. will it ever stop? 
