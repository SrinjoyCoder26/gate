# 📐 Engineering Mathematics - Last Minute Notes

## Quick Navigation
- [Discrete Mathematics](#discrete-mathematics)
- [Linear Algebra](#linear-algebra)
- [Calculus](#calculus)
- [Probability & Statistics](#probability--statistics)

---

> **GATE Weightage**: ~13% (13 marks) | **Expected Questions**: 4-6

---

# Discrete Mathematics

## 1. Propositional Logic

### Logical Connectives
| Connective | Symbol | Truth Condition |
|------------|--------|-----------------|
| AND | ∧ | True only when both are True |
| OR | ∨ | False only when both are False |
| NOT | ¬ | Inverts the truth value |
| IMPLIES | → | False only when T→F |
| BICONDITIONAL | ↔ | True when both same |

### 💡 Key Formulas

```
p → q ≡ ¬p ∨ q                    (Implication)
p ↔ q ≡ (p → q) ∧ (q → p)         (Biconditional)
¬(p ∧ q) ≡ ¬p ∨ ¬q                (De Morgan's)
¬(p ∨ q) ≡ ¬p ∧ ¬q                (De Morgan's)
```

### Tautology & Contradiction
- **Tautology**: Always TRUE (e.g., p ∨ ¬p)
- **Contradiction**: Always FALSE (e.g., p ∧ ¬p)
- **Contingency**: Neither tautology nor contradiction

### Important Equivalences
```
p → q ≡ ¬q → ¬p     (Contrapositive - LOGICALLY EQUIVALENT)
p → q ≢ q → p       (Converse - NOT EQUIVALENT)
p → q ≢ ¬p → ¬q     (Inverse - NOT EQUIVALENT)
```

---

## 2. Set Theory

### Basic Operations
| Operation | Symbol | Definition |
|-----------|--------|------------|
| Union | A ∪ B | Elements in A or B or both |
| Intersection | A ∩ B | Elements in both A and B |
| Difference | A - B | Elements in A but not in B |
| Complement | A' or Ācomplement | Elements not in A |
| Symmetric Difference | A ⊕ B | (A - B) ∪ (B - A) |

### 💡 Cardinality Formulas

```
|A ∪ B| = |A| + |B| - |A ∩ B|

|A ∪ B ∪ C| = |A| + |B| + |C| - |A∩B| - |B∩C| - |A∩C| + |A∩B∩C|

|Power Set| = 2^|A|

|A × B| = |A| × |B|
```

### Properties
- **A ∪ ∅ = A** (Identity)
- **A ∩ U = A** (Identity)
- **A ∪ A' = U** (Complement)
- **A ∩ A' = ∅** (Complement)

---

## 3. Relations

### Types of Relations
| Property | Definition | Example |
|----------|------------|---------|
| **Reflexive** | (a,a) ∈ R for all a | ≤, =, divides |
| **Symmetric** | (a,b) ∈ R ⇒ (b,a) ∈ R | =, sibling |
| **Transitive** | (a,b) ∈ R ∧ (b,c) ∈ R ⇒ (a,c) ∈ R | <, ≤, divides |
| **Anti-symmetric** | (a,b) ∈ R ∧ (b,a) ∈ R ⇒ a = b | ≤, divides |

### Special Relations
- **Equivalence Relation**: Reflexive + Symmetric + Transitive
- **Partial Order (POSET)**: Reflexive + Anti-symmetric + Transitive
- **Total Order**: POSET where every pair is comparable

### 💡 Counting Relations
```
Total relations on set A with n elements = 2^(n²)
Reflexive relations = 2^(n²-n) = 2^(n(n-1))
Symmetric relations = 2^(n(n+1)/2)
Reflexive & Symmetric = 2^(n(n-1)/2)
```

---

## 4. Functions

### Types of Functions
| Type | Definition | Condition |
|------|------------|-----------|
| **Injective (One-to-One)** | Different inputs → Different outputs | f(a) = f(b) ⇒ a = b |
| **Surjective (Onto)** | Every element in codomain has a preimage | Range = Codomain |
| **Bijective** | Both Injective and Surjective | One-to-one correspondence |

### 💡 Counting Functions (|A| = m, |B| = n)
```
Total functions from A to B = n^m

Injective functions = n!/(n-m)! = P(n,m)  [only if m ≤ n]

Surjective functions = n! × S(m,n)  [Stirling numbers]

Bijective functions = n!  [only if m = n]
```

---

## 5. Combinatorics

### Basic Counting Principles
```
Addition Principle: |A ∪ B| = |A| + |B| if A ∩ B = ∅
Multiplication Principle: |A × B| = |A| × |B|
```

### 💡 Permutations & Combinations

| Type | Formula | Use When |
|------|---------|----------|
| Permutation | P(n,r) = n!/(n-r)! | Order matters |
| Combination | C(n,r) = n!/[r!(n-r)!] | Order doesn't matter |
| Circular Permutation | (n-1)! | Arranging in circle |
| With Repetition (Perm) | n^r | Can repeat |
| With Repetition (Comb) | C(n+r-1, r) | Stars and bars |

### Important Identities
```
C(n,r) = C(n, n-r)                    (Symmetry)
C(n,r) = C(n-1,r-1) + C(n-1,r)        (Pascal's Identity)
Σ C(n,r) = 2^n                         (Sum of row)
C(n,0) + C(n,1) + ... + C(n,n) = 2^n
```

### Binomial Theorem
```
(x + y)^n = Σ C(n,r) × x^(n-r) × y^r
```

### Derangements (No element in original position)
```
D(n) = n! × [1 - 1/1! + 1/2! - 1/3! + ... + (-1)^n/n!]
D(n) = (n-1)[D(n-1) + D(n-2)]
D(1) = 0, D(2) = 1, D(3) = 2, D(4) = 9
```

---

## 6. Recurrence Relations

### Common Methods
1. **Substitution Method**
2. **Characteristic Equation Method**
3. **Master Theorem**

### 💡 Master Theorem
For T(n) = aT(n/b) + f(n) where a ≥ 1, b > 1:

| Case | Condition | Solution |
|------|-----------|----------|
| 1 | f(n) = O(n^(log_b(a) - ε)) | T(n) = Θ(n^(log_b(a))) |
| 2 | f(n) = Θ(n^(log_b(a))) | T(n) = Θ(n^(log_b(a)) × log n) |
| 3 | f(n) = Ω(n^(log_b(a) + ε)) | T(n) = Θ(f(n)) |

### Common Recurrences
```
T(n) = T(n-1) + 1         → O(n)         [Sequential search]
T(n) = T(n-1) + n         → O(n²)        [Selection sort]
T(n) = 2T(n-1) + 1        → O(2^n)       [Tower of Hanoi]
T(n) = T(n/2) + 1         → O(log n)     [Binary search]
T(n) = 2T(n/2) + n        → O(n log n)   [Merge sort]
T(n) = 2T(n/2) + 1        → O(n)         [Tree traversal]
T(n) = T(n/2) + n         → O(n)         [Quick select avg]
```

---

## 7. Graph Theory

### Basic Terminology
```
Degree of vertex v = Number of edges incident on v
Sum of degrees = 2 × |E|  (Handshaking Lemma)
In a tree: |E| = |V| - 1
```

### 💡 Important Graph Formulas

| Graph Type | Vertices | Edges | Max Edges |
|------------|----------|-------|-----------|
| Complete Graph K_n | n | n(n-1)/2 | n(n-1)/2 |
| Complete Bipartite K_{m,n} | m+n | m×n | m×n |
| Tree | n | n-1 | n-1 |
| Cycle C_n | n | n | n |
| Path P_n | n | n-1 | n-1 |

### Graph Properties
| Property | Definition |
|----------|------------|
| **Connected** | Path exists between every pair |
| **Eulerian Circuit** | Traverses every edge exactly once, returns to start |
| **Eulerian Path** | Traverses every edge exactly once |
| **Hamiltonian Circuit** | Visits every vertex exactly once, returns to start |
| **Hamiltonian Path** | Visits every vertex exactly once |

### Euler's Conditions
```
Eulerian Circuit exists ⟺ All vertices have EVEN degree
Eulerian Path exists ⟺ Exactly 0 or 2 vertices have ODD degree
```

### Planar Graphs - Euler's Formula
```
V - E + F = 2  (for connected planar graphs)

Where F = number of faces (including outer infinite face)

For simple connected planar graph:
E ≤ 3V - 6  (if V ≥ 3)
E ≤ 2V - 4  (if graph is bipartite)
```

### Graph Coloring
```
Chromatic number χ(G) = Minimum colors to color vertices
χ(Complete Graph K_n) = n
χ(Cycle C_n) = 2 if n is even, 3 if n is odd
χ(Tree) = 2 (for trees with ≥ 2 vertices)
χ(Bipartite) = 2
```

### Trees
```
Number of spanning trees in K_n = n^(n-2)  (Cayley's formula)
Binary tree with n nodes: height h where log₂(n+1)-1 ≤ h ≤ n-1
Full binary tree: Every node has 0 or 2 children
Complete binary tree: All levels filled except possibly last
```

---

# Linear Algebra

## 1. Matrices

### Types of Matrices
| Type | Property |
|------|----------|
| **Symmetric** | A = A^T |
| **Skew-Symmetric** | A = -A^T (diagonal = 0) |
| **Orthogonal** | A × A^T = I (A^(-1) = A^T) |
| **Idempotent** | A² = A |
| **Nilpotent** | A^k = 0 for some k |
| **Involutory** | A² = I |

### 💡 Matrix Properties
```
(AB)^T = B^T × A^T
(AB)^(-1) = B^(-1) × A^(-1)
det(AB) = det(A) × det(B)
det(A^T) = det(A)
det(kA) = k^n × det(A)  [for n×n matrix]
det(A^(-1)) = 1/det(A)
```

---

## 2. Determinants

### 💡 Properties of Determinants
```
1. Swapping two rows/columns → det changes sign
2. Multiplying a row by k → det multiplied by k
3. Adding multiple of one row to another → det unchanged
4. det(I) = 1
5. det(A) = 0 ⟺ A is singular (non-invertible)
6. det(triangular matrix) = product of diagonal elements
```

### 2×2 Determinant
```
|a b|
|c d| = ad - bc
```

### 3×3 Determinant (Sarrus Rule or Expansion)
```
|a b c|
|d e f| = a(ei-fh) - b(di-fg) + c(dh-eg)
|g h i|
```

---

## 3. Rank of Matrix

### 💡 Key Properties
```
Rank(A) = Number of non-zero rows in Row Echelon Form
Rank(A) ≤ min(m, n) for m×n matrix
Rank(A) = Rank(A^T)
Rank(AB) ≤ min(Rank(A), Rank(B))
```

### For System of Linear Equations Ax = b
```
Let [A|b] be augmented matrix:
- Rank(A) = Rank([A|b]) = n → Unique solution
- Rank(A) = Rank([A|b]) < n → Infinite solutions
- Rank(A) ≠ Rank([A|b]) → No solution
```

---

## 4. Eigenvalues & Eigenvectors

### 💡 Key Formulas
```
Characteristic equation: det(A - λI) = 0

Sum of eigenvalues = Trace(A) = sum of diagonal elements
Product of eigenvalues = det(A)

Eigenvalues of A^n = λ^n
Eigenvalues of A^(-1) = 1/λ
Eigenvalues of (A + kI) = λ + k
Eigenvalues of kA = kλ
```

### Properties
```
1. Similar matrices have same eigenvalues
2. Symmetric matrix → Real eigenvalues
3. Symmetric matrix → Orthogonal eigenvectors
4. Eigenvalues of triangular matrix = diagonal elements
5. If λ is eigenvalue of A with eigenvector v, then A^n has eigenvalue λ^n with same v
```

### Cayley-Hamilton Theorem
Every square matrix satisfies its own characteristic equation.

---

# Calculus

## 1. Limits

### 💡 Important Limits
```
lim(x→0) sin(x)/x = 1
lim(x→0) (1 - cos(x))/x = 0
lim(x→0) (1 + x)^(1/x) = e
lim(x→∞) (1 + 1/x)^x = e
lim(x→0) (e^x - 1)/x = 1
lim(x→0) (a^x - 1)/x = ln(a)
lim(x→0) ln(1 + x)/x = 1
lim(x→0) tan(x)/x = 1
```

### L'Hôpital's Rule
For indeterminate forms (0/0 or ∞/∞):
```
lim f(x)/g(x) = lim f'(x)/g'(x)
```

---

## 2. Derivatives

### 💡 Basic Derivatives
```
d/dx (x^n) = n × x^(n-1)
d/dx (e^x) = e^x
d/dx (a^x) = a^x × ln(a)
d/dx (ln x) = 1/x
d/dx (log_a x) = 1/(x × ln(a))
d/dx (sin x) = cos x
d/dx (cos x) = -sin x
d/dx (tan x) = sec²x
```

### Product & Quotient Rules
```
d/dx (uv) = u'v + uv'
d/dx (u/v) = (u'v - uv')/v²
```

### Chain Rule
```
d/dx [f(g(x))] = f'(g(x)) × g'(x)
```

---

## 3. Integration

### 💡 Basic Integrals
```
∫ x^n dx = x^(n+1)/(n+1) + C   [n ≠ -1]
∫ 1/x dx = ln|x| + C
∫ e^x dx = e^x + C
∫ a^x dx = a^x/ln(a) + C
∫ sin x dx = -cos x + C
∫ cos x dx = sin x + C
∫ sec²x dx = tan x + C
∫ 1/(1+x²) dx = tan⁻¹(x) + C
∫ 1/√(1-x²) dx = sin⁻¹(x) + C
```

### Integration by Parts
```
∫ u dv = uv - ∫ v du

ILATE Rule for choosing u:
I - Inverse trig
L - Logarithmic
A - Algebraic
T - Trigonometric
E - Exponential
```

---

## 4. Partial Derivatives

### 💡 Key Formulas
```
∂f/∂x: Treat y as constant, differentiate w.r.t x

Gradient: ∇f = (∂f/∂x, ∂f/∂y, ∂f/∂z)

Laplacian: ∇²f = ∂²f/∂x² + ∂²f/∂y² + ∂²f/∂z²
```

### Maxima/Minima for f(x,y)
```
Find critical points where ∂f/∂x = 0 and ∂f/∂y = 0

D = (∂²f/∂x²)(∂²f/∂y²) - (∂²f/∂x∂y)²

If D > 0 and ∂²f/∂x² > 0 → Local minimum
If D > 0 and ∂²f/∂x² < 0 → Local maximum
If D < 0 → Saddle point
If D = 0 → Inconclusive
```

---

# Probability & Statistics

## 1. Basic Probability

### 💡 Fundamental Rules
```
P(A') = 1 - P(A)
P(A ∪ B) = P(A) + P(B) - P(A ∩ B)
P(A ∩ B) = P(A) × P(B|A) = P(B) × P(A|B)

For independent events:
P(A ∩ B) = P(A) × P(B)

Bayes' Theorem:
P(A|B) = [P(B|A) × P(A)] / P(B)
```

### Conditional Probability
```
P(A|B) = P(A ∩ B) / P(B)
```

---

## 2. Random Variables

### Expectation (Mean)
```
E(X) = Σ xᵢ × P(xᵢ)           [Discrete]
E(X) = ∫ x × f(x) dx          [Continuous]

Properties:
E(aX + b) = a×E(X) + b
E(X + Y) = E(X) + E(Y)        [Always true]
E(XY) = E(X) × E(Y)           [Only if independent]
```

### Variance
```
Var(X) = E(X²) - [E(X)]²
Var(X) = E[(X - μ)²]

Properties:
Var(aX + b) = a² × Var(X)
Var(X + Y) = Var(X) + Var(Y)  [If independent]

Standard Deviation: σ = √Var(X)
```

---

## 3. Important Distributions

### 💡 Discrete Distributions

| Distribution | PMF | Mean | Variance |
|--------------|-----|------|----------|
| **Bernoulli** | P(X=1)=p, P(X=0)=1-p | p | p(1-p) |
| **Binomial** | C(n,k)p^k(1-p)^(n-k) | np | np(1-p) |
| **Geometric** | p(1-p)^(k-1) | 1/p | (1-p)/p² |
| **Poisson** | e^(-λ)λ^k/k! | λ | λ |

### 💡 Continuous Distributions

| Distribution | PDF | Mean | Variance |
|--------------|-----|------|----------|
| **Uniform(a,b)** | 1/(b-a) | (a+b)/2 | (b-a)²/12 |
| **Exponential(λ)** | λe^(-λx) | 1/λ | 1/λ² |
| **Normal(μ,σ²)** | Bell curve | μ | σ² |

### Normal Distribution Properties
```
68% within μ ± 1σ
95% within μ ± 2σ
99.7% within μ ± 3σ

Z-score: Z = (X - μ)/σ
```

---

## 4. Joint Probability

### 💡 Key Formulas
```
For independent X and Y:
P(X=x, Y=y) = P(X=x) × P(Y=y)
f(x,y) = f(x) × f(y)

Marginal Distribution:
P(X=x) = Σ P(X=x, Y=y)  over all y

Covariance:
Cov(X,Y) = E(XY) - E(X)E(Y)
Cov(X,Y) = 0 if X,Y are independent

Correlation:
ρ = Cov(X,Y) / (σ_X × σ_Y)
-1 ≤ ρ ≤ 1
```

---

## Quick Memory Tricks 🧠

1. **De Morgan's**: "Break the line, change the sign" (∧ ↔ ∨)
2. **Implication**: "p→q means if p then q; only false when T→F"
3. **Permutation vs Combination**: "P for Position matters"
4. **Binomial**: "n trials, each with probability p"
5. **Poisson**: "λ events in fixed interval, rare events"
6. **Eigenvalues**: "Sum = Trace, Product = Determinant"

---

## Common Mistakes to Avoid ⚠️

1. Confusing P(A|B) with P(B|A)
2. Forgetting to apply chain rule
3. Mixing up combinations and permutations
4. Wrong sign in De Morgan's law
5. Not checking if events are independent before using P(A∩B) = P(A)×P(B)
6. Forgetting to add +C in indefinite integrals
7. Confusing eigenvalue and eigenvector

---

## 📝 GATE Previous Year Patterns

### Most Frequently Asked Topics
1. **Probability** (Bayes' theorem, conditional probability) - 2-3 questions/year
2. **Graph Theory** (Euler path, chromatic number, trees) - 1-2 questions/year
3. **Linear Algebra** (Eigenvalues, rank, system of equations) - 2-3 questions/year
4. **Counting** (Permutations, combinations, recurrence) - 1-2 questions/year
5. **Propositional Logic** (Equivalences, satisfiability) - 1 question/year

### 💡 GATE-Style Practice Problems

**Problem 1 (Probability - GATE 2019 Pattern):**
```
A bag contains 3 red, 4 blue, and 5 green balls. Two balls are drawn 
without replacement. Find the probability that both balls are of different colors.

Solution:
P(different colors) = 1 - P(same color)
P(same red) = (3/12)(2/11) = 6/132
P(same blue) = (4/12)(3/11) = 12/132
P(same green) = (5/12)(4/11) = 20/132
P(same) = 38/132 = 19/66
P(different) = 1 - 19/66 = 47/66 ✓
```

**Problem 2 (Linear Algebra - GATE Pattern):**
```
For what value of k does the system have infinitely many solutions?
x + y + z = 6
x + 2y + 3z = 10
x + 2y + kz = 10

Solution:
For infinite solutions, Rank(A) = Rank([A|b]) < n
From row operations: k = 3 (third row becomes 0)
```

**Problem 3 (Graph Theory - GATE Pattern):**
```
A connected planar graph has 9 vertices with degree 4 each. 
Find the number of faces.

Solution:
Sum of degrees = 2E → 9 × 4 = 2E → E = 18
Using Euler's formula: V - E + F = 2
9 - 18 + F = 2 → F = 11 ✓
```

**Problem 4 (Combinatorics - GATE Pattern):**
```
In how many ways can 10 identical balls be distributed into 4 distinct boxes 
such that no box is empty?

Solution:
First place 1 ball in each box: remaining 6 balls, 4 boxes
Stars and bars: C(6 + 4 - 1, 4 - 1) = C(9, 3) = 84 ✓
```

---

## 📊 Formula Quick Reference Sheet

### Logic
```
p → q ≡ ¬p ∨ q ≡ ¬q → ¬p
p ↔ q ≡ (p → q) ∧ (q → p)
¬(p ∧ q) ≡ ¬p ∨ ¬q
¬(p ∨ q) ≡ ¬p ∧ ¬q
```

### Counting
```
Permutations: P(n,r) = n!/(n-r)!
Combinations: C(n,r) = n!/[r!(n-r)!]
Derangements: D(n) ≈ n!/e
Stars & Bars: C(n+r-1, r-1)
```

### Graphs
```
Σdegrees = 2|E|
Tree: |E| = |V| - 1
Planar: V - E + F = 2, E ≤ 3V - 6
Chromatic: χ(Kn) = n, χ(Cn) = 2 (even), 3 (odd)
Spanning trees in Kn = n^(n-2)
```

### Linear Algebra
```
Sum of eigenvalues = Trace(A)
Product of eigenvalues = det(A)
Rank + Nullity = n
```

### Probability
```
Bayes: P(A|B) = P(B|A)P(A)/P(B)
E(aX+b) = aE(X) + b
Var(aX+b) = a²Var(X)
Binomial mean = np, variance = np(1-p)
Poisson mean = variance = λ
```

### Calculus
```
L'Hôpital: lim f/g = lim f'/g'
Taylor: f(x) = Σ f^(n)(a)(x-a)^n/n!
```
