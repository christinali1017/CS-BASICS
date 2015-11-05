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


###External Sorting
---

External sorting is a term for a class of sorting algorithms that can handle **massive amounts of data**. External sorting is required when the data being sorted do not fit into the main memory of a computing device (usually RAM) and instead they must reside in the slower external memory (usually a hard drive). 

External sorting typically uses a hybrid sort-merge strategy. In the sorting phase, **chunks of data small enough to fit in main memory are read, sorted, and written out to a temporary file. In the merge phase, the sorted subfiles are combined into a single larger file.**

https://en.wikipedia.org/wiki/External_sorting