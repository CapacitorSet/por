go-por
======

A Golang implementation of publicly-verifiable proofs of retrievability, based on work by Shacham and Waters.

## Theory

The theory behind the proofs is detailed in *Compact Proofs of Retrievability*, by Hovav Shacham and Brent Waters. In particular, it implements the *Construction with RSA Signatures* detailed in section 6.

## Implementation

The current implementation tags the file `example.txt` with an RSA 2048-bit keypair (λ_1 - 1 = 2048), issues a verification request with l = 2 elements, and checks for its correctness.

## Example usage

```go
package main;

import (
	"fmt"
	"github.com/CapacitorSet/por"
	"os"
)

func main() {
	fmt.Printf("Generating RSA keys...\n")
	spk, ssk := Keygen()
	fmt.Printf("Generated!\n")

	fmt.Printf("Signing file...\n")
	file, err := os.Open("./example.txt")
	if err != nil {
		panic(err)
	}
	tau, authenticators := St(ssk, file)
	fmt.Printf("Signed!\n")

	fmt.Printf("Generating challenge...\n")
	q := Verify_one(tau, spk)
	fmt.Printf("Generated!\n")

	fmt.Printf("Issuing proof...\n")
	mu, sigma := Prove(q, authenticators, spk, file)
	fmt.Printf("Issued!\n")

	fmt.Printf("Verifying proof...\n")
	yes := Verify_two(tau, q, mu, sigma, spk)
	fmt.Printf("Result: %t!\n", yes)
	if yes {
		os.Exit(0)
	} else {
		os.Exit(1)
	}
}
```