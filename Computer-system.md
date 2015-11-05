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


