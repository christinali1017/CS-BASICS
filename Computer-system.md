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


**Provide protection**:

- One process can't interfere with another
- User process can't access privileged information


How virtual memory works?

**A page table maps virtual pages to physical pages.** 

- one page table entry(PTE) per virtual page.
- Each PTE specifies either a physical page or disk block address
- Each process has its own page table

**Address translation**

Basic Parameters
- N = 2^n : Number of addresses in virtual address space
- M = 2^m : Number of addresses in physical address space
- P = 2^p  : Page size (bytes)

Components of the virtual address (VA)
- TLBI: TLB index
- TLBT: TLB tag
- VPO: Virtual page offset
- VPN: Virtual page number

Components of the physical address (PA)
- PPO: Physical page offset (same as VPO)
- PPN:Physical page number
- CO: Byte offset within cache line
- CI:Cache index
- CT: Cache tag









