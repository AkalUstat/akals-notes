# 1. Binary Search
A fast and efficient way to search a *SORTED* array. We start with a min and max value.
1. Look at midpoint between first and last
2. if value > target, max = midpoint.
3. if value < target, min = midpoint

An *O(log n)* algorithm. 

# 2. Sorting

For this reason, and for others, it is useful to sort data.
### Attributes
1. Time Complexity (BigO).
2. Auxiliary space (some algos require extra memory).
3. Stable (elements of the same value retain their relative positions).
4. Online (data can be streamed in at algo runtime).

## A. Bubble Sort
One of the least efficient algos: Lighter elements bubble up and heavier items sink. There are two loops:
1. Outer from from start to end.
2. Inner loops runs from bottom up. It checks two neighbor elements and swaps them if they are out of order.
![[Screenshot 2023-10-04 at 11.24.45 AM.png]]

## B. Selection Sort
Selection sort is an evolution of the bubble sort. Instead of bubbling up one at a time, it scans the entire array, finds the smallest element, and swaps the values.
![[Screenshot 2023-10-04 at 11.27.28 AM.png]]

## C. Insertion Sort
Far more efficient than the previous two. It is like sorting a deck of cards (manually sorting). Start sorting on the left, find a card, move it, and move everything else right. Essentially, building a sorted array one at a time, above the outer loop.
1. Store the current value into a temp variable
2. Search all values that come before it. If it is smaller, it is moved up. 

No storage overhead, no swapping, and O(n) on sorted lists!
![[Screenshot 2023-10-04 at 11.31.32 AM.png]]
![[Screenshot 2023-10-04 at 11.32.14 AM.png]]

## D. Shell Sort
Broke the O($n^2$) barrier. In insertion sort, an element is moved one step closer to where it should be. Shell sort works the same logic but on larger distances with a *gap*. With each iteration, the gap decreases until 1, where adjacent elements are compared like an insertion sort. 

1. Sort all elements with gap $h_{k}$ relative to each other
2. repeat for $h_{k-1}$ until h = 1

Choosing a gap value:
1. relatively prime; best practical solution is an approximation of a relatively prime sequence.
The original algo uses gap of $k = \frac{N}{2}$ 
![[Screenshot 2023-10-04 at 11.37.01 AM.png]]![[Screenshot 2023-10-04 at 11.37.44 AM.png]]