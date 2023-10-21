Non-Comparative Sorting

# I. Dictionaries
A *collection* is a general term for a group of items, e.g. arrays, linked lists, stacks, queues, etc. While arrays are integer-indexed, we can use *dictionaries* as well, which are collections of objects indexed by other objects (key, value pairs). 
![[Screenshot 2023-10-04 at 7.30.41 PM.png]]

We want additions to be close to O(1) and access at O(log n), but there is no clear winner (foreshadowing).

#### Dictionaries vs. Databases
| | Dictionaries | Databases |
| ------ | ------- | --------- |
| keys | singe | many (e.g., name SSN, etc) |
| values | returns single | may return multiple |

# II. Bucket Sort
This sort uses the mathematical properties of keys. The algorithm creates a bucket for each of the different key values (often a queue or list) and items are placed into buckets), and then items are emptied back into the array. 
![[Screenshot 2023-10-04 at 7.35.33 PM.png]]

![[Screenshot 2023-10-04 at 7.35.44 PM.png]]

While making buckets for each individual key is expensive, making buckets for ranges of keys, sorting them, and then emptying them back is a way to optimize this.
![[Screenshot 2023-10-04 at 7.37.25 PM.png]]

# III. Radix Sort
Radix sort uses a bucket sort on each digit in the key (thus making the number of buckets always 10 for base 10 - wow! much save auxiliary complexity) either from the *L*east *S*ignificant *D*igit (LSD) or MSD. After each pass, the buckets are emptied and then we move onto the next digit in the number. 
![[Screenshot 2023-10-04 at 7.40.57 PM.png]]

Since radix sort has 10 buckets and creates an extra n array elements, our auxiliary complexity is O(b+n), and since we pass over the array *k* times, where k is the number of digits, our complexity is O(k $\cdot$ n). 