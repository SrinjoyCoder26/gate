# 🔤 Theory of Computation - Last Minute Notes

## Quick Navigation
- [Finite Automata](#finite-automata)
- [Regular Languages](#regular-languages)
- [Context-Free Grammar](#context-free-grammar)
- [Pushdown Automata](#pushdown-automata)
- [Turing Machines](#turing-machines)
- [Decidability](#decidability)

---

# Finite Automata

## 1. Deterministic Finite Automata (DFA)

### 💡 DFA Definition
```
DFA = (Q, Σ, δ, q₀, F)

Q   = Finite set of states
Σ   = Input alphabet
δ   = Transition function: Q × Σ → Q
q₀  = Initial state (q₀ ∈ Q)
F   = Set of final/accepting states (F ⊆ Q)
```

### DFA Properties
```
• For each state and input symbol, exactly ONE transition
• No ε (epsilon) transitions
• Complete specification: transition for every (state, symbol) pair
• Dead state: Non-accepting state with self-loops
```

### 💡 Minimum States for DFA
```
Strings of length exactly n over Σ = {a, b}: n + 2 states
Strings of length at least n: n + 1 states
Strings divisible by n: n states
nth symbol from end is 'a': 2^n states
Contains substring 'w' of length n: Roughly n + 1 states
```

---

## 2. Non-Deterministic Finite Automata (NFA)

### 💡 NFA Definition
```
NFA = (Q, Σ, δ, q₀, F)

δ = Q × (Σ ∪ {ε}) → 2^Q  (Power set of Q)

Differences from DFA:
• Multiple transitions for same input (or none)
• ε-transitions allowed
• Accepts if ANY path leads to final state
```

### NFA Properties
```
• At least ONE accepting path → Accept
• All paths reject → Reject
• More compact than equivalent DFA
```

---

## 3. NFA to DFA Conversion (Subset Construction)

### 💡 Algorithm
```
1. Start state of DFA = ε-closure(start state of NFA)
2. For each DFA state S and input a:
   - New state = ε-closure(∪ δ(q, a) for all q ∈ S)
3. DFA final states = states containing any NFA final state
4. Repeat until no new states

Worst case: 2^n DFA states for n-state NFA
```

### ε-Closure
```
ε-closure(q) = Set of all states reachable from q using only ε-transitions
             = {q} ∪ (all states reachable via ε from q)
```

---

## 4. DFA Minimization

### 💡 Table Filling (Myhill-Nerode) Algorithm
```
1. Mark all pairs (final, non-final)
2. For unmarked pair (p, q):
   If (δ(p,a), δ(q,a)) is marked for any a ∈ Σ:
   Mark (p, q)
3. Repeat step 2 until no new marks
4. Unmarked pairs → equivalent states → merge

Minimum DFA states = number of equivalence classes
```

### Myhill-Nerode Theorem
```
L is regular ⟺ L has finite number of equivalence classes
Number of states in minimum DFA = number of equivalence classes
```

---

# Regular Languages

## 1. Regular Expressions

### 💡 RE Operators (by precedence)
```
1. Parentheses ()    - Highest
2. Kleene star *     
3. Concatenation     
4. Union +  (or |)   - Lowest

Basic operations:
• a        - Matches 'a'
• ε        - Empty string
• ∅        - Empty language
• R₁ + R₂  - Union (R₁ or R₂)
• R₁R₂     - Concatenation
• R*       - Zero or more times
• R⁺       - One or more (= RR*)
```

### 💡 RE Identities
```
R + ∅ = R           (Identity for union)
R · ε = ε · R = R   (Identity for concatenation)
R · ∅ = ∅ · R = ∅   (Annihilator)
R + R = R           (Idempotent)
R* = ε + RR*        (Definition)
R* = (ε + R)*
(R*)* = R*
ε* = ε
∅* = ε
(R + S)* = (R*S*)*
```

### 💡 Common Regular Expressions
| Language | Regular Expression |
|----------|-------------------|
| Strings starting with a | a(a+b)* |
| Strings ending with b | (a+b)*b |
| Strings containing ab | (a+b)\*ab(a+b)* |
| Strings with even a's | (b\*ab*ab\*)* |
| Strings with odd a's | b\*a(b\*ab*ab\*)* |
| All strings | (a+b)* |
| Strings of even length | ((a+b)(a+b))* |

---

## 2. Pumping Lemma for Regular Languages

### 💡 Statement
```
If L is regular, then ∃ pumping length p such that:
For any string w ∈ L with |w| ≥ p:
w can be divided as w = xyz where:
1. |xy| ≤ p
2. |y| > 0
3. For all i ≥ 0: xy^i z ∈ L
```

### Using Pumping Lemma to Prove Non-Regular
```
1. Assume L is regular
2. Let p be the pumping length
3. Choose w ∈ L with |w| ≥ p (adversarial choice)
4. For ANY division xyz satisfying |xy| ≤ p, |y| > 0:
   Find i such that xy^i z ∉ L
5. Contradiction → L is not regular
```

### 💡 Non-Regular Languages
```
• {aⁿbⁿ | n ≥ 0}           - Equal a's and b's
• {ww | w ∈ {a,b}*}        - Repeat string
• {aⁿ | n is prime}        - Prime length
• {aⁿ | n is perfect square}
• {aⁿbᵐ | n ≠ m}
• {aⁿbᵐ | n < m}
• Balanced parentheses
```

---

## 3. Closure Properties of Regular Languages

### 💡 Regular Languages are CLOSED under:
```
✓ Union (L₁ ∪ L₂)
✓ Intersection (L₁ ∩ L₂)
✓ Concatenation (L₁L₂)
✓ Kleene Star (L*)
✓ Complement (L̄)
✓ Difference (L₁ - L₂)
✓ Reversal (Lᴿ)
✓ Homomorphism
✓ Inverse Homomorphism
```

### 💡 Closure Tricks
```
L₁ ∩ L₂ = complement(complement(L₁) ∪ complement(L₂))
L₁ - L₂ = L₁ ∩ complement(L₂)
```

---

# Context-Free Grammar

## 1. CFG Definition

### 💡 CFG Components
```
G = (V, T, P, S)

V = Variables (Non-terminals)
T = Terminals
P = Production rules
S = Start symbol (S ∈ V)

Production: A → α where A ∈ V, α ∈ (V ∪ T)*
```

### Example
```
S → aSb | ε
Generates: {ε, ab, aabb, aaabbb, ...} = {aⁿbⁿ | n ≥ 0}
```

---

## 2. Chomsky Normal Form (CNF)

### 💡 CNF Rules
```
Every production is of the form:
1. A → BC (two non-terminals)
2. A → a (single terminal)
3. S → ε (only if ε ∈ L)

No unit productions (A → B)
No ε-productions (except S → ε)
```

### Conversion to CNF
```
1. Eliminate ε-productions
2. Eliminate unit productions
3. Replace terminals in RHS with new variables
4. Break long productions into binary

CFG with n variables → CNF with O(n²) productions
```

### 💡 CYK Algorithm Uses CNF
```
Time: O(n³|G|) for string of length n
Uses dynamic programming
```

---

## 3. Greibach Normal Form (GNF)

### 💡 GNF Rules
```
Every production is of the form:
A → aα where a is terminal, α is string of non-terminals

Used for LL(1) parsing and PDA construction
```

---

## 4. Ambiguity

### 💡 Ambiguous Grammar
```
A grammar is ambiguous if:
∃ string w with TWO or more different:
• Leftmost derivations, OR
• Rightmost derivations, OR
• Parse trees
```

### Inherently Ambiguous Language
```
No unambiguous grammar exists for the language
Example: {aⁿbⁿcᵐdᵐ | n,m ≥ 1} ∪ {aⁿbᵐcᵐdⁿ | n,m ≥ 1}
```

---

## 5. Pumping Lemma for CFLs

### 💡 Statement
```
If L is CFL, then ∃ pumping length p such that:
For any string w ∈ L with |w| ≥ p:
w can be divided as w = uvxyz where:
1. |vxy| ≤ p
2. |vy| > 0
3. For all i ≥ 0: uv^i xy^i z ∈ L
```

### 💡 Non-CFLs
```
• {aⁿbⁿcⁿ | n ≥ 0}      - Can't pump all three equally
• {ww | w ∈ {a,b}*}      - Copy language
• {aⁿbⁿcⁿdⁿ | n ≥ 0}
• {aⁱbʲcᵏ | i < j < k}
```

---

## 6. Closure Properties of CFLs

### 💡 CFLs are CLOSED under:
```
✓ Union (L₁ ∪ L₂)
✓ Concatenation (L₁L₂)
✓ Kleene Star (L*)
✓ Reversal (Lᴿ)
✓ Homomorphism
✓ Substitution
```

### 💡 CFLs are NOT CLOSED under:
```
✗ Intersection (L₁ ∩ L₂)
✗ Complement (L̄)
✗ Difference (L₁ - L₂)
```

### 💡 Important Exception
```
CFL ∩ Regular = CFL
(Intersection with regular language IS closed)
```

---

# Pushdown Automata

## 1. PDA Definition

### 💡 PDA Components
```
PDA = (Q, Σ, Γ, δ, q₀, Z₀, F)

Q  = Finite set of states
Σ  = Input alphabet
Γ  = Stack alphabet
δ  = Transition function: Q × (Σ ∪ {ε}) × Γ → 2^(Q × Γ*)
q₀ = Initial state
Z₀ = Initial stack symbol
F  = Final states
```

### Transition Notation
```
δ(q, a, X) = {(p, γ), ...}

From state q, reading input a, stack top X:
Go to state p, replace X with γ

γ = ε means pop
γ = YZ means replace X with YZ (Z on top)
```

---

## 2. Acceptance Modes

### 💡 Two Acceptance Modes
```
1. Acceptance by Final State:
   Accept if in final state after reading entire input
   Stack contents don't matter

2. Acceptance by Empty Stack:
   Accept if stack is empty after reading entire input
   Final states don't matter

Both modes are equivalent in power!
```

---

## 3. DPDA vs NPDA

### 💡 Deterministic PDA (DPDA)
```
At most one move possible at any configuration

DPDA can recognize:
• All regular languages
• Some CFLs (e.g., aⁿbⁿ)

DPDA cannot recognize:
• Some CFLs (e.g., palindromes over {a,b})
```

### 💡 Languages Hierarchy
```
Regular ⊂ DCFL ⊂ CFL

DCFL (Deterministic CFL):
• LR grammars
• Closed under complement
• NOT closed under union, intersection with CFL
```

---

# Turing Machines

## 1. TM Definition

### 💡 TM Components
```
TM = (Q, Σ, Γ, δ, q₀, B, F)

Q = States
Σ = Input alphabet
Γ = Tape alphabet (Σ ⊂ Γ)
δ = Q × Γ → Q × Γ × {L, R}
q₀ = Initial state
B = Blank symbol (B ∈ Γ - Σ)
F = Final states
```

### Transition
```
δ(q, a) = (p, b, D)

In state q, reading a:
• Go to state p
• Write b
• Move head in direction D (Left or Right)
```

---

## 2. TM Configurations

### 💡 Instantaneous Description (ID)
```
ID = αqβ

α = tape content to left of head
q = current state
β = tape content from head position to right (includes current symbol)

Example: aabqbba means head at first 'b', state q
```

---

## 3. TM Variants

### 💡 All Equivalent in Power
```
• Standard TM
• Multi-tape TM (simulate with single tape)
• Non-deterministic TM (simulate with deterministic)
• Two-way infinite tape
• Multi-dimensional tape
• Multi-head TM
• Offline TM (read-only input tape)

All recognize same languages: Recursively Enumerable Languages
```

### Multi-tape TM Simulation
```
k-tape TM simulated by 1-tape TM
Time blowup: O(t²) for t steps
Space: Same
```

---

## 4. Chomsky Hierarchy

### 💡 Four Types of Languages
| Type | Language | Machine | Grammar |
|------|----------|---------|---------|
| 3 | Regular | DFA/NFA | Right/Left linear |
| 2 | Context-Free | PDA | A → α |
| 1 | Context-Sensitive | LBA | αAβ → αγβ, |γ| ≥ 1 |
| 0 | Recursively Enumerable | TM | α → β |

### 💡 Memory Trick
```
Type 3 ⊂ Type 2 ⊂ Type 1 ⊂ Type 0

"Regular Children Can Read"
Regular ⊂ Context-Free ⊂ Context-Sensitive ⊂ Recursively Enumerable
```

---

# Decidability

## 1. Language Classes

### 💡 Key Definitions
```
Decidable (Recursive):
• TM always halts
• Says YES or NO

Semi-Decidable (Recursively Enumerable - RE):
• TM halts on YES
• May loop forever on NO

Undecidable:
• No TM can decide
```

### 💡 Relationship
```
Recursive ⊂ RE

L is Recursive ⟺ L and L̄ are both RE
If L is RE but L̄ is not RE → L is not Recursive
```

---

## 2. Decidability of Problems

### 💡 Decidable Problems
| Language | Problem | Decidable? |
|----------|---------|------------|
| Regular | Membership, Emptiness, Equivalence, Finiteness | ✓ |
| CFL | Membership, Emptiness | ✓ |
| CFL | Equivalence, Ambiguity | ✗ |
| Recursive | Membership | ✓ |
| RE | Membership | Semi-decidable |

### Decision Table
```
             Membership  Emptiness  Finiteness  Equivalence
Regular         ✓           ✓           ✓            ✓
CFL             ✓           ✓           ✓            ✗
CSL             ✓           ✗           ✗            ✗
Recursive       ✓           ✗           ✗            ✗
RE              ~           ✗           ✗            ✗

✓ = Decidable
✗ = Undecidable
~ = Semi-decidable
```

---

## 3. Undecidable Problems

### 💡 Famous Undecidable Problems
```
1. Halting Problem:
   Given TM M and input w, does M halt on w?

2. Blank Tape Halting:
   Given TM M, does M halt on blank tape?

3. State Entry Problem:
   Given TM M, input w, state q, does M ever enter q?

4. Rice's Theorem:
   Every non-trivial property of RE languages is undecidable

5. Post Correspondence Problem (PCP):
   Given sequences, can we make matching strings?

6. Equivalence of CFGs:
   Are two CFGs equivalent?

7. Ambiguity of CFG:
   Is given CFG ambiguous?
```

### 💡 Rice's Theorem
```
Any non-trivial property of the language recognized by TM is undecidable.

Non-trivial: Some TMs have it, some don't
Property of language: Depends only on language, not TM

Example undecidable:
• Is L(M) empty?
• Is L(M) regular?
• Is L(M) = Σ*?
• Is L(M) finite?
```

---

## 4. Reduction

### 💡 Reduction Concept
```
A ≤ B means A reduces to B

If A ≤ B and B is decidable → A is decidable
If A ≤ B and A is undecidable → B is undecidable

Used to prove undecidability:
Reduce known undecidable problem to new problem
```

---

## Quick Memory Tricks 🧠

1. **Chomsky Hierarchy**: "Type number goes up, power goes up"
2. **Pumping Lemma**: "Regular pumps in first p, CFL pumps in middle"
3. **CNF**: "Binary tree productions - two NTs or one T"
4. **CFLs closed under**: "Union, Concat, Star, Reversal" (not intersection, complement)
5. **Regular but not CFL**: Impossible! (Regular ⊂ CFL)
6. **Rice's Theorem**: "Any language property of TM is undecidable"

---

## 💡 Quick Decision Flowchart

```
Is language finite?
├─ Yes → Regular (and CFL, decidable)
└─ No → Continue checking

Can count be bounded?
├─ No pumping works → Check higher types
├─ aⁿbⁿ type → CFL (not regular)
├─ aⁿbⁿcⁿ type → Not CFL
└─ ww type → Not CFL

Is it decidable?
├─ Has algorithm → Recursive
├─ TM exists but may not halt → RE
└─ No TM possible → Not RE
```

---

## Common Mistakes to Avoid ⚠️

1. Confusing NFA (multiple paths OK) with DPDA (single path)
2. Pumping lemma proves non-regularity, not regularity
3. CFLs NOT closed under intersection (but CFL ∩ Regular = CFL)
4. Forgetting |xy| ≤ p constraint in regular pumping lemma
5. Confusing decidable (always halts) with semi-decidable (may loop)
6. Not all CFLs are DCFLs (palindromes need NPDA)
7. Rice's theorem only for language properties, not TM properties
