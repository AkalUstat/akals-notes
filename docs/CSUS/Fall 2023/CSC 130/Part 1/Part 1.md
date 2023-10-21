Algorithm Analysis

# 1. Analysis of Algorithms

## A. What is an Algorithm?
An *algorithm* is a sequence of unambiguous instructions that solve a problem. An *instance* of an algorithm is specified by a unique set of data fed to it. 

*Algorithmics* analyses these algorithms in terms of: correctness, unambiguity, effectiveness, and finiteness. 

#### Correctness
Correctness means that the algorithm produces the exact/valid output for valid input (does what it is supposed to do). There are two proofs for algorithms:
1. ***Proof of Correctness***: If the algorithm produces the correct output for each input. Ease of proof depends on the algorithm
2. ***Proof of Incorrectness***: Easiest to prove. Find just one instance where the algorithm fails.

#### Effectiveness
Ok, the algorithm does what it is supposed to do. But is it good? We analyze: 
- ***Time efficiency***: How long the algorithm takes to complete
- ***Space efficiency***: How much memory and resources will be needed.
And how they change as the data set grows (better algos will be better in each).

## B. Time Complexity Basics
We analyze time complexity by the *number of repetitions* of the ***basic operation***, which contributes most to the running time, as a function of input size (n).
$$ T(n) \approx C_{op}C(n) $$
Where $T(n)$ is the total execution time as a function of the number of items in the data set, $C_{op}$ is the execution time of the basic operation, and $C(n)$ is the number of times the basic operation executes.

***Worst Case $C_{worst}(n)$***: maximum number of executions over a set of size n. (rare)
***Best case $C_{best}(n)$***: minimum executions over a set of size n. (rare).
***Average Case $C_{avg}(n)$***: how executes using typical data (NOT the average of the worst and best case)

## C. Order of Growth

How the function grows as $n\rightarrow \infty$ . Can depend on: form of input, number of inputs, computer speed, etc. *Rate of Growth* is the curvature of the line associated with the function. There are:
- Constant (1)
- Log($\approx log  n$)
- Linear (n)
- Log Linear ($\approx n log n$)
- Quadratic ($n^2$)
- Exponential ($2^n$)

There are three types of notations: 
![[Screenshot 2023-10-02 at 4.42.35 PM.png]]
But, we will only focus on Big-O

## 4. Big O
This the upper-bound of algo growth. 

***O(1)***: Constant algorithm. It does not increase/decrease based on size of n. 
**O($log n$)***: Increases with n, but at a decreasing rate.
***O(n)***: Grows linearly with n (Biggest ex: interation)
***O($n log n$)***: Log linear growth. n * logn growth (Ex: Quick, Heap, Merge sort & Fourier transform)
***O($n^2$)***: n * n growth. Not great for large values of n (Ex: Bubble Sort, Selection Sort, merging unsorted arrays, matrix multiplication)
***O($2^n$)***:
![[Screenshot 2023-10-02 at 4.48.01 PM.png]]

## 5. BigO Math
1. Find worst-case number of primitive operations executed as function of input size
2. eliminate meaningless values, keep largest power of n.

## 6. Towers of Hanoi
$2^n -1$. 
