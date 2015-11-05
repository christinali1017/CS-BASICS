###What is hashing technique? Describe in brief.
---
In general, in all searching techniques, search time is dependent on the number of items. Sequential search, binary search and all the search trees are totally dependent on number of items and many key comparisons are involved.

**Hashing is a technique where search time is independent of the number of items or elements. In this technique a hash function is used to generate an address from a key. The hash function takes a key as input and returns the hash value of that key which is used as an address index in the array.**

**Techniques for making hash function.**

- **Truncation Method**: In this method we take only a part of the key as address.
- **Midsquare Method**: In this method the key is squared and some digits from the middle of this square are taken as address.
- **Folding Method**: In this technique the key is divided into different part where the length of each part is same as that of the required address, except possibly the last part.
- **Division Method(Modulo-Division)**: In Modulo-Division method the key is mod by the table size and the remainder is taken as the address of the hash table.


**Collision resolution**:



http://www.careerride.com/Data-Structure-Interview-Questions.aspx

