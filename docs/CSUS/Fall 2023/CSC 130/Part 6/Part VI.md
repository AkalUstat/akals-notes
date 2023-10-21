Recursive Sorting

# I. Merging Arrays
O(n) for both time and space complexity.

#### Steps
1. Keep two counters (one for each).
2. Loop while both arrays have data.
	1. Smaller element is put into the auxiliary array.
	2. increment that array's counter which lost the element
3. After the loop
	1. One array will still have elements, so append them to the auxiliary array.

# II. Merge Sort: Divide and Conquer
A recursive algorithm. 
#### Algorithm
As the recursion bubbles back up , each sublist is merged. This 3D aspect (sorted at each level with an O(n) iteration, and then with O(log n) number of recursions) means this algorithm is O(n log n) with O(n) space complexity.

##### Recursion:
1. While elements are > 2, split array in half and recurse.
2. Base Case: If 1 element, it is sorted. If two, arbitrary swap.

![[Screenshot 2023-10-04 at 11.45.25 AM.png]]

# III. Quick Sort: Pivoting
Choose a "pivot" element in the array (generally using the first item). 

#### Algorithm
Partition the values based on smaller than or greater than. Start with "Bigger than" pointer immediately after the pivot, and the "Smaller than" pointer at the end of the array, and then swap elements when each finds a value that matches its requirements. They will collide and then "Smaller than" will move past "Bigger than", at which point it is swapped with the pivot. Then, recurse on the two arrays (Bigger than and smaller than). 
![[Screenshot 2023-10-04 at 11.47.42 AM.png]]

#### Worst Case
Array is already sorted. If the first item is chosen, the sub-array will have all n - 1 elements while the other will be empty. One way to minimize the chance of this is to manually randomize. O(n) loop from start to end and swap with $i$ and a random index.
![[Screenshot 2023-10-04 at 11.51.20 AM.png]]