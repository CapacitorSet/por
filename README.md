go-por
======

A Golang implementation of publicly-verifiable proofs of retrievability, based on work by Shacham and Waters.

## Theory

The theory behind the proofs is detailed in *Compact Proofs of Retrievability*, by Hovav Shacham and Brent Waters. In particular, it implements the *Construction with RSA Signatures* detailed in section 6.

## Implementation

The current implementation tags the file `example.txt` with an RSA 2048-bit keypair (λ_1 - 1 = 2048), issues a verification request with l = 2 elements, and checks for its correctness.