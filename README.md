# Ordered Four Squares with Parity Constraints

Efficient solution for representing a natural number as a sum of four squares with specified parity constraints and strict ordering.

## Description

The code finds solutions to the equation:

$$n = a_1^2 + a_2^2 + a_3^2 + a_4^2$$

subject to the following conditions:

- Strict ordering: $$a_1 > a_2 > a_3 > a_4 \geq 0 $$
- Specified parity for each $$a_i$$ (even or odd)
- Includes Lagrange optimization for all-even cases

## Jacobi’s Four-Square Theorem

This algorithm is closely related to **Jacobi’s classical four-square theorem**, which gives an exact formula for the number of representations of a natural number as a sum of four squares.

Jacobi proved that the number of representations of an integer *n* can be expressed as:


$$
r_4(n)=8\sum\limits_{\substack{d\mid n\ d\neq 0\ \bmod\ 4}} d
$$

In other words, to count how many ways *n* can be written as a sum of four squares, you sum over all divisors of *n* that are **not** multiples of 4, multiply each divisor by 8, and that’s the result.

This algorithm can compute **explicit representations** — not just the count — making it useful in computational research related to modular forms and number theory.

---

## Modular Forms and Connections

**Modular forms** play a central role in modern number theory.  
They appear in areas such as the proof of **Fermat’s Last Theorem** and the study of **elliptic curves**.

The four-square problem is deeply connected to **theta functions**, which are among the earliest and most fundamental examples of modular forms.  
By generating concrete four-square decompositions, this algorithm contributes to the computational exploration of modular and theta function structures.

## Key Features

### Search Algorithm

- Descending search with efficient branch pruning
- Modular arithmetic (mod $$2^k$$) for fast reachability checks
- Precomputed suffix sums of quadratic residues
- Reduction via division by powers of 4 for fully-even solutions


### Performance

- Parameter `k=7` (mod 128) balances pruning accuracy with speed
- DFS with early exit on first solution found
- Optimized bounds for minimal tail sums


## Usage

```python
from four_squares import find_ordered_four_squares_with_lagrange

# Find representation of 130 with even a1, a2 and odd a3, a4
result = find_ordered_four_squares_with_lagrange(
    n=130,
    p1='even',
    p2='even', 
    p3='odd',
    p4='odd',
    k=7
)

if result:
    a1, a2, a3, a4 = result
    print(f"{130} = {a1}² + {a2}² + {a3}² + {a4}²")
else:
    print("No solution found")
```


## Function Parameters

**`find_ordered_four_squares_with_lagrange(n, p1, p2, p3, p4, k=7)`**

- `n` — target number to represent
- `p1, p2, p3, p4` — parity for each term (`'even'` or `'odd'`)
- `k` — modular arithmetic parameter (default 7, mod 128)

**Returns:** tuple `(a1, a2, a3, a4)` or `None` if no solution exists

## Requirements

- Python 3.6+
- Standard library (`math` module)


## Theoretical Foundation

Based on Lagrange's four-square theorem with additional constraints. Uses reduction for even solutions: if all $$a_i$$ are even, then  $$n \equiv 0 \pmod{4}$$, and we can factor out powers of 4.

## License

Apache License 2.0

***
