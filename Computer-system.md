###How float is stored
---

With single precision:

- Sign bit : 1 bit
- e : exponent 7 bit
- m : magnitude 23 bit

With the above representation, we have:
- denormalized: (−1)signbits×2−126× 0.significandbits
- normalized: (−1)signbits×2exponentbits−127× 1.significandbits
- NAN: exponent 11111... significand non-zero
- Infinity: exponent 11111... significand zero


###Virtual memory
---

Why virtual memory?

**Provide the illusion of very very large main memory.** 
- Store bulk of data on disk, use physical DRAM as a cache for the disk
- Address space of a process can exceed physical memory
- Sum of address spaces of multiple processes can exceed physical memory.


**Simplify memory management**

- multiple processes reside in main memory
- only active code and data is actually in memory






