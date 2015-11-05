###Quicksort vs Mergesort
---

- Time complexity
  * quicksort average : O(nlogn) Worst case : O(n ^ 2)
  * Mergesort average : O(nlogn) Worst case : O(nlogn)
  * Quicksort is faster in practice than other O(nlogn) algorithm.
- Space
  * Mergesort: O(N)
  * Quicksort in place if we don't count the recursive space.
- **Quicksort is typically faster than mergesort when the data is stored in memory**. However, when the sata set is huge and is stored on external devices such as a hard drive, merge sort is the clear winner in terms of speed. It minimizes the expensive reads of the external drive and also lends itself well to parallel computing.