go-por
======

A Golang implementation of publicly-verifiable proofs of retrievability, based on work by Shacham and Waters.

## Theory

The theory behind the proofs is detailed in *Compact Proofs of Retrievability*, by Hovav Shacham and Brent Waters. In particular, it implements the *Construction with RSA Signatures* detailed in section 6.

## Implementation

The current implementation verifies a simple string of 9 bits, namely `0b010101010`, with p = 61, n = 53, e = 17, d = 2753. It splits the file into a 3x3 grid of bits, and signs it with name = 3, u1 = u2 = u3 = 2, and issues tau without signing tau0. It then issues a verification request with l = 2, Q = {(i = 0, vi = 1), (i = 2, vi = 2)}, answers the request, and verifies the answer.