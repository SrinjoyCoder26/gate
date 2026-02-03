# 🔤 Theory of Computation - Last Minute Notes

## Quick Navigation
- [Finite Automata](#finite-automata)
- [Regular Languages](#regular-languages)
- [Context-Free Grammar](#context-free-grammar)
- [Pushdown Automata](#pushdown-automata)
- [Turing Machines](#turing-machines)
- [Decidability](#decidability)

---

> **GATE Weightage**: ~6-8% (6-8 marks) | **Expected Questions**: 4-5

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

---

## 📝 GATE Previous Year Patterns

### Most Frequently Asked Topics
1. **DFA/NFA Construction & Minimization** - 2-3 questions/year
2. **Regular Expressions** - 1-2 questions/year
3. **Pumping Lemma** - 1 question/year
4. **CFG/CFL Properties** - 1-2 questions/year
5. **Decidability** - 1 question/year
6. **Turing Machines** - 1 question/year

### 💡 GATE-Style Practice Problems

**Problem 1 (DFA - GATE Pattern):**
```
Construct minimum DFA for strings over {0,1} with:
- Number of 0s is divisible by 2, AND
- Number of 1s is divisible by 3

Solution:
Need to track (0s mod 2, 1s mod 3)
States: (0,0), (0,1), (0,2), (1,0), (1,1), (1,2)

Minimum states = 2 × 3 = 6 states

Start: (0,0)
Final: (0,0)

Transitions:
(i,j) on 0 → ((i+1)mod2, j)
(i,j) on 1 → (i, (j+1)mod3)
```

**Problem 2 (NFA to DFA - GATE Pattern):**
```
NFA: States {q0, q1, q2}, Start: q0, Final: q2
Transitions: 
δ(q0, a) = {q0, q1}
δ(q0, b) = {q0}
δ(q1, b) = {q2}

Subset construction:
[q0] --a--> [q0,q1]  --b--> [q0,q2]*
[q0] --b--> [q0]
[q0,q1] --a--> [q0,q1]  
[q0,q1] --b--> [q0,q2]*
[q0,q2] --a--> [q0,q1]
[q0,q2] --b--> [q0]

DFA states: {[q0], [q0,q1], [q0,q2]*}
Minimum DFA = 3 states ✓
```

**Problem 3 (Regular Expression - GATE Pattern):**
```
Write RE for strings over {a,b} NOT containing "aa".

Solution:
Can have: single a followed by b(s), or just b(s)
Pattern: (b + ab)*(a + ε)

Or equivalently: b*(ab+b)*a? 
Or: (b + ab)*(ε + a) ✓

Verification:
✓ ε (empty)
✓ a 
✓ b
✓ ab
✓ ba
✓ aba
✗ aa (rejected - correct!)
```

**Problem 4 (Pumping Lemma - GATE Pattern):**
```
Prove L = {aⁿbⁿcⁿ | n ≥ 0} is not context-free.

Proof:
Assume L is CFL. Let p be pumping length.
Choose w = aᵖbᵖcᵖ ∈ L, |w| = 3p ≥ p

For any division w = uvxyz with |vxy| ≤ p, |vy| > 0:
- vxy cannot contain both a's and c's (|vxy| ≤ p)
- So vy contains at most 2 types of symbols

Pumping: uv²xy²z will have unequal counts of a, b, c
Therefore, uv²xy²z ∉ L

Contradiction! L is not CFL. ✓
```

**Problem 5 (CFG - GATE Pattern):**
```
Convert to CNF: S → aAB | bBA, A → aS | a, B → bS | b

Step 1: Remove ε-productions (none here)
Step 2: Remove unit productions (none here)
Step 3: Replace terminals in long productions
  Introduce: Ca → a, Cb → b
  
Step 4: Convert to binary productions
S → CaX1 | CbX2 where X1 → AB, X2 → BA
A → CaS | a
B → CbS | b

CNF:
S → CaX1 | CbX2
X1 → AB
X2 → BA
A → CaS | a
B → CbS | b
Ca → a
Cb → b ✓
```

**Problem 6 (Decidability - GATE Pattern):**
```
Which of the following is decidable?

a) Is L(M) = Σ* for TM M?
b) Is L(M) empty for TM M?
c) Is L(G) empty for CFG G?
d) Is L(M) regular for TM M?

Solution:
a) Undecidable (Rice's theorem - non-trivial property)
b) Undecidable (Rice's theorem)
c) ✓ Decidable! (Check if start symbol generates anything)
d) Undecidable (Rice's theorem)

Answer: c ✓
```

**Problem 7 (Minimum States - GATE Pattern):**
```
Minimum DFA states for language:
"Strings over {a,b} where 3rd symbol from end is 'a'"

Solution:
Need to remember last 3 symbols.
Each position can be 'a' or 'b'.
States = 2³ = 8 states

For "nth symbol from end is 'a'" → 2ⁿ states ✓
```

**Problem 8 (Closure Properties - GATE Pattern):**
```
If L1 is regular and L2 is CFL, which is always CFL?

a) L1 ∩ L2
b) L1 ∪ L2
c) L1 - L2
d) L2 - L1

Solution:
a) ✓ CFL (CFL ∩ Regular = CFL)
b) ✓ CFL (CFL ∪ Regular ⊆ CFL)
c) May not be CFL
d) ✓ CFL (L2 ∩ L1' where L1' is regular)

All except c are always CFL.
```

---

## 📊 Formula Quick Reference Sheet

### DFA/NFA State Counts
```
Minimum DFA for:
- Strings divisible by n: n states
- nth symbol from end = a: 2ⁿ states
- Contains substring w (length k): k+1 states
- Ends with substring w: |w|+1 states
```

### Language Hierarchy
```
Regular ⊂ DCFL ⊂ CFL ⊂ CSL ⊂ RE ⊂ All Languages

Machine equivalence:
Regular = DFA = NFA = RE = Right-linear grammar
CFL = NPDA = CFG
CSL = LBA
RE = TM
```

### Closure Properties
```
Operation    | Regular | CFL  | CSL  | RE
-------------|---------|------|------|-----
Union        |   ✓     |  ✓   |  ✓   |  ✓
Intersection |   ✓     |  ✗   |  ✓   |  ✓
Complement   |   ✓     |  ✗   |  ✓   |  ✗
Concatenation|   ✓     |  ✓   |  ✓   |  ✓
Kleene Star  |   ✓     |  ✓   |  ✓   |  ✓
Homomorphism |   ✓     |  ✓   |  ?   |  ✓

Special: CFL ∩ Regular = CFL
         DCFL is closed under complement
```

### Decidability Table
```
Problem          | Regular | CFL  | CSL  | RE
-----------------|---------|------|------|-----
Membership       |   ✓     |  ✓   |  ✓   |  ~
Emptiness        |   ✓     |  ✓   |  ✗   |  ✗
Finiteness       |   ✓     |  ✓   |  ✗   |  ✗
Equivalence      |   ✓     |  ✗   |  ✗   |  ✗
Ambiguity        |   N/A   |  ✗   |  ✗   |  ✗
Universality     |   ✓     |  ✗   |  ✗   |  ✗

✓ = Decidable, ✗ = Undecidable, ~ = Semi-decidable
```

### Pumping Lemmas
```
Regular (|w| ≥ p):
w = xyz where |xy| ≤ p, |y| > 0
xy^i z ∈ L for all i ≥ 0

CFL (|w| ≥ p):
w = uvxyz where |vxy| ≤ p, |vy| > 0
uv^i xy^i z ∈ L for all i ≥ 0
```

### Grammar Forms
```
CNF (Chomsky Normal Form):
A → BC or A → a or S → ε

GNF (Greibach Normal Form):
A → aα where α ∈ (non-terminals)*

For n-length string w:
CYK with CNF: O(n³) time
Number of derivation steps: 2n-1
```

---

## 💡 Additional Important Topics

### Linear Bounded Automata (LBA)
```
Turing Machine with tape limited to input length
- Tape cells: O(n) where n = input length
- Recognizes Context-Sensitive Languages

LBA ⊂ TM in power
CSL = L(LBA)

LBA cannot simulate itself (unlike TM)
```

### Post's Correspondence Problem (PCP)
```
Given: List of domino pairs (top, bottom)
Question: Can we arrange dominoes so top string = bottom string?

Example:
Domino 1: (a, ab)
Domino 2: (b, ca)
Domino 3: (ca, a)

No solution possible - PCP is undecidable!

Used to prove: CFG ambiguity is undecidable
```

### Kleene's Theorem
```
Three equivalent representations of regular languages:
1. Finite Automata (DFA/NFA)
2. Regular Expressions
3. Regular Grammar (Right-linear or Left-linear)

Conversions:
- RE → NFA: Thompson's construction
- NFA → DFA: Subset construction
- DFA → RE: State elimination
- FA ↔ Regular Grammar: Direct construction
```

### Arden's Theorem
```
For regular expression equation: X = AX + B
Solution: X = A*B (if ε ∉ A)

Used to convert DFA/NFA to Regular Expression:
1. Write equations for each state
2. Solve using Arden's theorem
3. Get RE for final state
```

### Properties of Regular Languages
```
Solvable decision problems:
- Membership: Is w ∈ L? - O(n) for DFA
- Emptiness: Is L = ∅? - Check reachability to final state
- Finiteness: Is L finite? - Check for cycles to final state
- Equivalence: Is L₁ = L₂? - Minimize and compare

Counting:
- Number of strings of length exactly n
- Uses transfer matrix method or generating functions
```

### Properties of Context-Free Languages
```
Deterministic CFL (DCFL):
- Recognized by DPDA
- Closed under complement
- LR(k) grammars generate DCFLs
- DCFL ⊂ CFL (proper subset)

Inherently Ambiguous Languages:
- No unambiguous grammar exists
- Example: {aⁿbⁿcᵐdᵐ} ∪ {aⁿbᵐcᵐdⁿ}
```

### Turing Machine Variations
```
Multi-tape TM:
- Multiple read/write heads
- Same power as single-tape
- Can be simulated with O(t²) slowdown

Non-deterministic TM:
- Multiple possible transitions
- Same power as deterministic TM
- Can be simulated with exponential slowdown

Two-way Infinite Tape:
- Tape extends infinitely in both directions
- Same power as standard TM

Random Access TM:
- Can jump to any tape position
- Same power as standard TM
```

### Computable Functions
```
Recursive Functions = Computable Functions:
- Computed by some Turing Machine

Church-Turing Thesis:
- Any "effectively computable" function is TM-computable

Busy Beaver Function:
- Maximum steps before halting for n-state TM
- Not computable (grows faster than any computable function)
```

### 💡 More GATE-Style Practice Problems

**Problem 9 (LBA - GATE Pattern):**
```
Which of the following is recognized by LBA but not by PDA?

a) {aⁿbⁿ | n ≥ 0}
b) {aⁿbⁿcⁿ | n ≥ 0}
c) {aⁿ | n is prime}
d) Both b and c

Solution:
a) aⁿbⁿ - CFL, can be done by PDA
b) aⁿbⁿcⁿ - CSL, NOT CFL, needs LBA
c) Primes - Can be computed in linear space, so CSL

Answer: d) Both b and c ✓
```

**Problem 10 (Arden's Theorem - GATE Pattern):**
```
Find RE for DFA with states {q0, q1, q2}:
- q0 initial, q2 final
- δ(q0, a) = q1, δ(q0, b) = q0
- δ(q1, a) = q2, δ(q1, b) = q0
- δ(q2, a) = q2, δ(q2, b) = q2

Solution:
Equations:
q0 = ε + q0·b + q1·b (start + return paths)
q1 = q0·a
q2 = q1·a + q2·a + q2·b = q1·a + q2·(a+b)

From Arden's: q2 = q1·a·(a+b)*
              q1 = q0·a
So: q2 = q0·a·a·(a+b)* = q0·aa(a+b)*

From q0 = ε + q0·b = b* (Arden's)
Final: q2 = b*aa(a+b)* ✓
```

**Problem 11 (Rice's Theorem Application - GATE Pattern):**
```
Which is decidable?
a) Does TM M halt on empty input?
b) Does TM M have exactly 100 states?
c) Is L(M) = {a}?
d) Is L(M) context-free?

Solution:
Rice's Theorem: Non-trivial properties of L(TM) are undecidable

a) Halting on empty - About behavior, undecidable
b) Number of states - About TM structure, not language
   This is DECIDABLE! Just count states.
c) L(M) = {a} - Language property, undecidable
d) L(M) is CFL - Language property, undecidable

Answer: b ✓
```
