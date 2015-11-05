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

**External merge sort**:

One example of external sorting is the external merge sort algorithm, which sorts chunks that each fit in RAM, then merges the sorted chunks together. For example, for sorting 900 megabytes of data using only 100 megabytes of RAM:

Read 100 MB of the data in main memory and sort by some conventional method, like quicksort.
Write the sorted data to disk.

Repeat steps 1 and 2 until all of the data is in sorted 100 MB chunks (there are 900MB / 100MB = 9 chunks), which now need to be merged into one single output file.

Read the first 10 MB (= 100MB / (9 chunks + 1)) of each sorted chunk into input buffers in main memory and allocate the remaining 10 MB for an output buffer. (In practice, it might provide better performance to make the output buffer larger and the input buffers slightly smaller.)

Perform a 9-way merge and store the result in the output buffer. Whenever the output buffer fills, write it to the final sorted file and empty it. Whenever any of the 9 input buffers empties, fill it with the next 10 MB of its associated 100 MB sorted chunk until no more data from the chunk is available. 

https://en.wikipedia.org/wiki/External_sorting