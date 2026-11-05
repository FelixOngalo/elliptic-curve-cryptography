# Elliptic Curve Cryptography: Mathematical Theory and Implementation in R

## Overview

This project explores the mathematical foundations of **Elliptic Curve Cryptography (ECC)** through rigorous mathematical arguments, computational verification and implementation from scratch.

The study focuses on elliptic curves over finite fields, the algebraic structure of their points, cryptographic key agreement and the computational difficulty of the elliptic curve discrete logarithm problem.

The project connects number theory, abstract algebra, finite fields, group theory and computational complexity to practical cryptographic applications.

The implementation is developed at toy scale to make the underlying mathematics transparent and verifiable.

## Mathematical Foundations

### 1. Elliptic Curves over Finite Fields

The project studies elliptic curves of the form:

\[
E(\mathbb F_p): y^2=x^3+ax+b\pmod p
\]

where \(p\) is prime and the curve satisfies the non-singularity condition:

\[
4a^3+27b^2\not\equiv0\pmod p.
\]

The points on the curve, together with the point at infinity, form an abelian group under the elliptic-curve group law.

### 2. The Elliptic-Curve Group Law

The group operation is defined geometrically using the chord-and-tangent construction.

The project develops the point-addition and point-doubling formulas and establishes the closure property.

**Closure of the group law:** The chord-and-tangent formulas return another point on the curve. The proof substitutes the line equation into the cubic curve equation, obtains a polynomial whose roots correspond to the intersection points, and applies Vieta's formulas to establish the coordinates of the resulting point.

The group identity and inverse operations are also examined.

**Associativity:** The associativity of elliptic-curve addition is a deeper result. Rather than presenting an incomplete proof, the report identifies the relevant mathematical references and distinguishes this cited theorem from the properties proved directly in the project.

### 3. Prime-Order Subgroups

The project examines the role of subgroups in elliptic-curve cryptography.

By Lagrange's theorem, the order of an element divides the order of its finite group.

In particular, if a subgroup has prime order \(r\), every non-identity element generates the entire subgroup.

This property is fundamental to selecting cryptographic generators and understanding the structure of elliptic-curve public keys.

### 4. Elliptic Curve Diffie–Hellman (ECDH)

The project demonstrates how two participants can independently calculate the same shared elliptic-curve point.

Let \(G\) be a public generator point.

Alice chooses a private integer \(a\) and calculates:

\[
A=aG.
\]

Bob chooses a private integer \(b\) and calculates:

\[
B=bG.
\]

Their shared points are:

\[
S_A=aB=a(bG)
\]

and

\[
S_B=bA=b(aG).
\]

Using associativity of scalar multiplication and commutativity of integer multiplication:

\[
a(bG)=(ab)G=(ba)G=b(aG).
\]

Therefore:

\[
\boxed{S_A=S_B}
\]

The report establishes the correctness of the key-agreement construction, conditional on the elliptic-curve group properties, including associativity.

### 5. Elliptic Curve Discrete Logarithm Problem

The security of ECC relies on the computational difficulty of recovering an integer \(k\) from:

\[
Q=kG.
\]

This is the Elliptic Curve Discrete Logarithm Problem (ECDLP).

The project compares two approaches:

- **Brute-force search:** Tests candidate scalar values sequentially, requiring approximately \(r/2\) operations on average for a subgroup of order \(r\).
- **Baby-step giant-step (BSGS):** Uses a time-memory trade-off to solve the discrete logarithm in approximately \(O(\sqrt r)\) group operations and \(O(\sqrt r)\) storage.

For a subgroup of approximately 256-bit prime order, generic square-root attacks require approximately 128-bit security work.

This explains why elliptic-curve cryptography can provide strong security with comparatively smaller key sizes than traditional RSA systems.

## Mathematical Results: Proofs and Verification

An important feature of this project is the distinction between results established through mathematical proofs, results supported by cited theorems, and results checked computationally.

| Result | Treatment |
|---|---|
| Closure of the elliptic-curve group law | Proved |
| Lagrange's theorem and prime-order subgroup consequences | Proved |
| ECDH key-agreement correctness | Proved, conditional on group associativity |
| Baby-step giant-step algorithm | Proved |
| Associativity of elliptic-curve addition | Cited from established mathematical literature |
| Hasse's theorem | Proof sketch and numerical verification |

**Mathematical qualification:** The correctness of ECDH depends on associativity. Since associativity is cited rather than independently proved in this project, the key-agreement proof relies on that established group-theoretic result.

Hasse's theorem provides a bound on the number of points on an elliptic curve over a finite field:

\[
\left|\#E(\mathbb F_p)-(p+1)\right|\leq2\sqrt p.
\]

The project includes a proof sketch and computational checks against enumerated curve points.

## Computational Implementation

The implementation explores the mathematical constructions through independent computational experiments.

The principal areas include:

- Elliptic-curve point enumeration over finite fields.
- Point addition and point doubling.
- Scalar multiplication.
- Subgroup generation and order verification.
- Elliptic-curve key agreement.
- Baby-step giant-step discrete logarithm attacks.
- Comparison of brute-force and BSGS computational scaling.
- Numerical verification of Hasse's point-count bound.

The code is intentionally implemented at toy scale so that the mathematical operations can be inspected and verified.

## Security Considerations and Limitations

This project is an educational implementation, not production-ready cryptographic software.

The implementation has important limitations:

- It operates on small finite fields for computational experimentation.
- It is not designed to execute in constant time.
- It does not implement comprehensive public-key validation.
- It does not provide production-grade side-channel protection.
- It does not implement the full security requirements of a real cryptographic protocol.

**Never use the implementation to protect real private keys, financial transactions or sensitive information.**

Production cryptographic systems require thoroughly reviewed implementations, secure parameter selection, point validation, appropriate key handling and resistance to timing and other side-channel attacks.

## Academic References

1. Silverman, J. H. *The Arithmetic of Elliptic Curves*. Springer.
2. Washington, L. C. *Elliptic Curves: Number Theory and Cryptography*. Chapman & Hall/CRC.
3. Koblitz, N. *A Course in Number Theory and Cryptography*. Springer.
4. NIST. *FIPS 186-5: Digital Signature Standard*.

These references support the deeper mathematical theory and the transition from elliptic-curve group structures to practical cryptographic constructions.

## Key Learning Outcomes

This project develops an understanding of:

- Finite fields and elliptic curves over prime fields.
- Algebraic group structures and subgroup generation.
- Elliptic-curve point addition and scalar multiplication.
- Lagrange's theorem and its cryptographic implications.
- Elliptic Curve Diffie–Hellman key agreement.
- The Elliptic Curve Discrete Logarithm Problem.
- Baby-step giant-step algorithms and computational complexity.
- Hasse's theorem and elliptic-curve point counting.
- The relationship between mathematical assumptions and cryptographic security.
