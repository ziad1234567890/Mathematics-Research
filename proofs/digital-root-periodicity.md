# Digital Root Periodicity in Base-10 Arithmetic
## Theorem and Proof
### Author: [YOUR NAME]
### Date: [TODAY'S DATE]

---

## 1. Statement of Theorem

**Theorem 1.1** (Digital Root Periodicity)
For all natural numbers \(n\), the digital root of \(3n\) is constrained to the set \(\{3, 6, 9\}\):

\[
\forall n \in \mathbb{N}, \quad dr(3n) \in \{3, 6, 9\}
\]

Where \(dr(x)\) denotes the digital root of \(x\) in base 10.

---

## 2. Preliminary Definitions

**Definition 2.1** (Digital Root)
The digital root \(dr(n)\) of a natural number \(n\) is defined recursively as:

\[
dr(n) = 
\begin{cases} 
n & \text{if } 0 \leq n \leq 9 \\
dr(S(n)) & \text{otherwise}
\end{cases}
\]

where \(S(n)\) is the sum of the digits of \(n\) in base 10.

**Definition 2.2** (Congruence Relation)
Equivalently, the digital root can be expressed using modular arithmetic:

\[
dr(n) \equiv n \pmod{9}, \quad dr(n) \neq 0 \Rightarrow dr(n) \in \{1,2,\dots,9\}
\]

with the convention that \(dr(n) = 9\) when \(n \equiv 0 \pmod{9}\).

---

## 3. Proof

### 3.1 Modular Arithmetic Approach

Let \(n \in \mathbb{N}\). Consider \(3n \mod 9\):

\[
3n \equiv 0, 3, \text{ or } 6 \pmod{9}
\]

since:
- If \(n \equiv 0 \pmod{3}\), then \(3n \equiv 0 \pmod{9}\)
- If \(n \equiv 1 \pmod{3}\), then \(3n \equiv 3 \pmod{9}\)
- If \(n \equiv 2 \pmod{3}\), then \(3n \equiv 6 \pmod{9}\)

### 3.2 Digital Root Interpretation

From Definition 2.2:
1. If \(3n \equiv 0 \pmod{9}\), then \(dr(3n) = 9\)
2. If \(3n \equiv 3 \pmod{9}\), then \(dr(3n) = 3\)
3. If \(3n \equiv 6 \pmod{9}\), then \(dr(3n) = 6\)

Thus, \(dr(3n) \in \{3, 6, 9\}\).

### 3.3 Direct Computational Verification (Python)

```python
def digital_root(n: int) -> int:
    """Calculate digital root of n."""
    return 1 + ((n - 1) % 9) if n > 0 else 0

def verify_theorem(limit: int = 1000) -> bool:
    """Verify Theorem 1.1 for n = 1 to limit."""
    for n in range(1, limit + 1):
        dr = digital_root(3 * n)
        if dr not in {3, 6, 9}:
            return False, n, dr
    return True, None, None

# Verification
valid, counterexample, value = verify_theorem(1000)
print(f"Theorem holds for first 1000 natural numbers: {valid}")
if not valid:
    print(f"Counterexample: n={counterexample}, dr(3n)={value}")
