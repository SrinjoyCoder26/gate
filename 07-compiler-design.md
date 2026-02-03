# 🔧 Compiler Design - Last Minute Notes

## Quick Navigation
- [Lexical Analysis](#lexical-analysis)
- [Syntax Analysis](#syntax-analysis)
- [Syntax Directed Translation](#syntax-directed-translation)
- [Intermediate Code](#intermediate-code)
- [Code Optimization](#code-optimization)
- [Code Generation](#code-generation)

---

> **GATE Weightage**: ~5-6% (5-6 marks) | **Expected Questions**: 3-4

---

# Compiler Overview

## 💡 Phases of Compiler
```
Source Code
    ↓
┌─────────────────────────────────────────┐
│ ANALYSIS PHASE (Front End)              │
│  1. Lexical Analysis → Tokens           │
│  2. Syntax Analysis → Parse Tree        │
│  3. Semantic Analysis → Annotated Tree  │
└─────────────────────────────────────────┘
    ↓
Intermediate Code
    ↓
┌─────────────────────────────────────────┐
│ SYNTHESIS PHASE (Back End)              │
│  4. Intermediate Code Generation        │
│  5. Code Optimization                   │
│  6. Code Generation → Target Code       │
└─────────────────────────────────────────┘

Symbol Table: Used by ALL phases
Error Handler: Invoked by all phases
```

---

# Lexical Analysis

## 1. Lexical Analyzer (Scanner)

### 💡 Functions
```
1. Read source program character by character
2. Group characters into lexemes
3. Produce tokens (token-name, attribute-value)
4. Remove whitespace and comments
5. Report lexical errors
6. Interact with symbol table
```

### Token Examples
```
Source: position = initial + rate * 60

Tokens:
<id, 1>         position
<assign_op>     =
<id, 2>         initial
<add_op>        +
<id, 3>         rate
<mul_op>        *
<num, 60>       60
```

---

## 2. Regular Expressions → NFA → DFA

### 💡 Thompson's Construction (RE → NFA)
```
Base cases:
• ε: Two states with ε-transition
• a: Two states with 'a' transition

Inductive cases:
• r₁|r₂: New start → ε → (r₁ NFA or r₂ NFA) → ε → new final
• r₁r₂: Connect r₁ final to r₂ start
• r*: ε to r NFA, ε back from r final to r start, ε to bypass
```

### Subset Construction (NFA → DFA)
```
See Theory of Computation notes
Time: O(2^n) states in worst case
```

---

## 3. Lexical Errors

### 💡 Error Recovery Strategies
```
1. Panic Mode: Skip characters until valid token found
2. Delete character
3. Insert missing character
4. Replace character
5. Transpose adjacent characters
```

---

# Syntax Analysis

## 1. Context-Free Grammars

### 💡 Grammar Classification
```
Unambiguous: Unique parse tree for each string
Ambiguous: Multiple parse trees possible

Left Recursive: A → Aα | β
Right Recursive: A → αA | β
```

### Removing Left Recursion
```
Before: A → Aα | β
After:  A → βA'
        A' → αA' | ε

General: A → Aα₁ | Aα₂ | β₁ | β₂
Convert: A → β₁A' | β₂A'
         A' → α₁A' | α₂A' | ε
```

### Left Factoring
```
Before: A → αβ₁ | αβ₂
After:  A → αA'
        A' → β₁ | β₂
```

---

## 2. FIRST and FOLLOW

### 💡 FIRST Set
```
FIRST(X) = Set of terminals that can begin strings derived from X

Rules:
1. If X is terminal: FIRST(X) = {X}
2. If X → ε: Add ε to FIRST(X)
3. If X → Y₁Y₂...Yₖ:
   - Add FIRST(Y₁) - {ε} to FIRST(X)
   - If ε ∈ FIRST(Y₁), add FIRST(Y₂) - {ε}
   - Continue until Yᵢ doesn't derive ε
   - If all derive ε, add ε
```

### 💡 FOLLOW Set
```
FOLLOW(A) = Set of terminals that can appear immediately after A

Rules:
1. Add $ to FOLLOW(Start symbol)
2. If A → αBβ: Add FIRST(β) - {ε} to FOLLOW(B)
3. If A → αB, or A → αBβ where ε ∈ FIRST(β):
   Add FOLLOW(A) to FOLLOW(B)
```

---

## 3. Parsing Techniques

### 💡 Parser Comparison
| Parser | Type | Direction | Power |
|--------|------|-----------|-------|
| Recursive Descent | Top-down | Left | LL(1) |
| LL(1) | Top-down | Left | LL(1) |
| LR(0) | Bottom-up | Right | LR(0) |
| SLR(1) | Bottom-up | Right | SLR(1) |
| LALR(1) | Bottom-up | Right | LALR(1) |
| CLR(1)/LR(1) | Bottom-up | Right | LR(1) |

### 💡 Parser Hierarchy
```
LL(1) ⊂ LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ LR(1)

Every LL(1) grammar is LR(1)
Not every LR(1) grammar is LL(1)
```

---

## 4. LL(1) Parsing

### 💡 LL(1) Conditions
```
Grammar is LL(1) if for every production A → α | β:
1. FIRST(α) ∩ FIRST(β) = ∅
2. If ε ∈ FIRST(α), then FIRST(β) ∩ FOLLOW(A) = ∅
3. At most one of α, β can derive ε
```

### LL(1) Parse Table Construction
```
For each production A → α:
1. For each terminal a ∈ FIRST(α):
   Add A → α to M[A, a]
2. If ε ∈ FIRST(α):
   For each terminal b ∈ FOLLOW(A):
   Add A → α to M[A, b]

Conflict → Not LL(1)
```

### 💡 LL(1) Grammars CANNOT have:
```
• Left recursion
• Common prefixes (need left factoring)
• Ambiguity
```

---

## 5. LR Parsing

### 💡 LR Parsing Overview
```
L = Left-to-right scan
R = Rightmost derivation (in reverse)

Uses stack and parsing table
Actions: Shift, Reduce, Accept, Error
```

### LR(0) Items
```
An item is a production with a dot (•)
A → •XYZ (nothing parsed)
A → X•YZ (X parsed)
A → XYZ• (complete item, ready to reduce)
```

### 💡 Closure and Goto
```
CLOSURE(I):
1. Add all items in I
2. For each item A → α•Bβ in closure:
   Add B → •γ for all productions B → γ

GOTO(I, X):
For each item A → α•Xβ in I:
Add A → αX•β to GOTO(I, X)
Then take closure
```

---

## 6. SLR(1) Parser

### 💡 SLR Parse Table Construction
```
1. Construct LR(0) items and canonical collection
2. For each state I:
   - If A → α•aβ ∈ I, GOTO(I,a) = Iⱼ: ACTION[i,a] = shift j
   - If A → α• ∈ I, A ≠ S': ACTION[i,b] = reduce (for all b ∈ FOLLOW(A))
   - If S' → S• ∈ I: ACTION[i,$] = accept
3. For non-terminal A: GOTO[i,A] = j if GOTO(Iᵢ,A) = Iⱼ

Conflict → Not SLR(1)
```

---

## 7. CLR(1) / LR(1) Parser

### 💡 LR(1) Items
```
Item format: [A → α•β, a]
a = lookahead symbol

More states than LR(0)
Reduces only when lookahead matches
Most powerful (recognizes all LR grammars)
```

---

## 8. LALR(1) Parser

### 💡 LALR(1) Construction
```
1. Construct LR(1) items
2. Merge states with same core (ignore lookaheads)
3. Combine lookaheads for merged states

Same number of states as SLR(1)
More powerful than SLR(1)
Used by YACC/Bison
```

### 💡 Conflict Types
```
Shift-Reduce Conflict:
Both shift and reduce possible in a state

Reduce-Reduce Conflict:
Multiple reductions possible in a state

SLR < LALR < CLR in handling conflicts
```

---

## 9. Operator Precedence Parsing

### 💡 Precedence Relations
```
a ⋖ b : a has lower precedence than b (a yields to b)
a ⋗ b : a has higher precedence than b (a takes from b)
a ≐ b : a and b have equal precedence
```

### Handle Finding
```
Scan left for ⋖
Scan right for ⋗
Contents between ⋖ and ⋗ form the handle
```

---

# Syntax Directed Translation

## 1. SDT Concepts

### 💡 Attribute Types
```
Synthesized Attribute:
• Computed from children
• Can be used with any grammar
• Value flows up the parse tree

Inherited Attribute:
• Computed from parent/siblings
• Cannot be used with LR parsing
• Value flows down the parse tree
```

### 💡 S-Attributed vs L-Attributed
```
S-Attributed Definition:
• Only synthesized attributes
• Can be evaluated bottom-up
• Compatible with LR parsing

L-Attributed Definition:
• Synthesized attributes, OR
• Inherited attributes depend only on:
  - Inherited attributes of parent
  - Attributes of left siblings
• Can be evaluated left-to-right, depth-first
• Compatible with LL parsing
```

---

## 2. Annotated Parse Tree

### Example: Expression Evaluation
```
Production          Semantic Rule
E → E₁ + T          E.val = E₁.val + T.val
E → T               E.val = T.val
T → T₁ * F          T.val = T₁.val * F.val
T → F               T.val = F.val
F → (E)             F.val = E.val
F → digit           F.val = digit.lexval
```

---

# Intermediate Code

## 1. Three Address Code (TAC)

### 💡 TAC Forms
```
x = y op z          Binary operation
x = op y            Unary operation
x = y               Copy
goto L              Unconditional jump
if x goto L         Conditional jump
if x relop y goto L Conditional jump
x = y[i]            Array access
x[i] = y            Array assignment
x = &y              Address
x = *y              Dereference
*x = y              Indirect assignment
param x             Parameter passing
call p, n           Procedure call with n params
return y            Return value
```

### Types of TAC Representation
```
1. Quadruples: (op, arg1, arg2, result)
2. Triples: (op, arg1, arg2) - result is triple number
3. Indirect Triples: Array of pointers to triples
```

---

## 2. Static Single Assignment (SSA)

```
Each variable assigned exactly once
Uses φ (phi) functions at join points

Example:
x = 1               x₁ = 1
x = 2               x₂ = 2
x = x + 1           x₃ = x₂ + 1
```

---

# Code Optimization

## 1. Optimization Levels

### 💡 Machine Independent vs Dependent
```
Machine Independent:
• Common subexpression elimination
• Dead code elimination
• Constant folding/propagation
• Loop optimization
• Strength reduction

Machine Dependent:
• Register allocation
• Instruction scheduling
• Peephole optimization
```

---

## 2. Basic Block and Control Flow

### 💡 Basic Block
```
A sequence of statements where:
• Control enters only at first statement
• Control leaves only from last statement
• No jumps into or out of middle
```

### Finding Basic Blocks
```
Leaders (start of basic block):
1. First statement
2. Target of any goto
3. Statement following any goto

Basic block = leader + all statements until next leader
```

---

## 3. Local Optimizations

### 💡 Common Optimizations
```
1. Common Subexpression Elimination:
   t1 = a + b          t1 = a + b
   t2 = a + b    →     t2 = t1

2. Dead Code Elimination:
   Remove code that doesn't affect output

3. Constant Folding:
   x = 3 + 4     →     x = 7

4. Constant Propagation:
   x = 5               
   y = x + 3     →     y = 8

5. Copy Propagation:
   x = y               
   z = x + 1     →     z = y + 1

6. Strength Reduction:
   x * 2         →     x << 1
   x * 8         →     x << 3
   x / 2         →     x >> 1
```

---

## 4. Loop Optimizations

### 💡 Loop Optimization Techniques
```
1. Code Motion (Loop Invariant):
   Move computation outside loop if result doesn't change

2. Induction Variable Elimination:
   Replace induction variable with simpler computation

3. Strength Reduction in Loops:
   Replace multiplication with addition

4. Loop Unrolling:
   Reduce loop overhead by replicating body

5. Loop Fusion:
   Combine adjacent loops with same bounds
```

---

## 5. Data Flow Analysis

### 💡 Reaching Definitions
```
A definition d reaches point p if:
• There's a path from d to p
• d is not killed (redefined) along path

gen[B] = definitions generated in B
kill[B] = definitions killed in B
IN[B] = reaching definitions at entry of B
OUT[B] = reaching definitions at exit of B

OUT[B] = gen[B] ∪ (IN[B] - kill[B])
IN[B] = ∪ OUT[P] for all predecessors P
```

### 💡 Liveness Analysis
```
Variable x is live at point p if:
• There's a path from p to a use of x
• x is not defined along that path

def[B] = variables defined in B
use[B] = variables used before definition in B
IN[B] = variables live at entry of B
OUT[B] = variables live at exit of B

IN[B] = use[B] ∪ (OUT[B] - def[B])
OUT[B] = ∪ IN[S] for all successors S
```

---

# Code Generation

## 1. Target Code Forms
```
1. Absolute machine code
2. Relocatable machine code
3. Assembly language
```

---

## 2. Register Allocation

### 💡 Graph Coloring Approach
```
1. Build interference graph
   - Node for each variable
   - Edge if both live at same time
2. Color graph with k colors (k = registers)
3. If can't color, spill variable to memory
```

### 💡 Register Descriptor & Address Descriptor
```
Register Descriptor:
Track which variables are in which registers

Address Descriptor:
Track where each variable's value is stored
```

---

## 3. Instruction Selection

### 💡 Simple Code Generation
```
For x = y op z:
1. Get y into register R
2. Perform R = R op z
3. Store R in x if needed
```

### Next-Use Information
```
Used to decide:
• Which value to keep in register
• Which value to spill

If variable not used later, don't keep in register
```

---

## Quick Memory Tricks 🧠

1. **Compiler phases**: "Lexical → Syntax → Semantic → IC → Optimize → Code Gen"
2. **LL(1)**: "No Left recursion, No common Left factors"
3. **LR parsers**: "L0 < SLR < LALR < CLR" (increasing power)
4. **FIRST/FOLLOW**: "FIRST for what starts, FOLLOW for what follows"
5. **S-attributed**: "Synthesized only, flows up"
6. **L-attributed**: "Left-to-right, works with LL"

---

## 💡 Parser Power Summary

```
Grammar Type → Parser
LL(1) → Recursive Descent, Predictive
LR(0) → Simple LR
SLR(1) → Simple LR with FOLLOW
LALR(1) → Most practical (YACC)
LR(1) → Most powerful, most states
```

---

## Common Mistakes to Avoid ⚠️

1. Forgetting to compute FOLLOW before making LL(1) table
2. Confusing shift-reduce with reduce-reduce conflicts
3. Not removing left recursion before LL parsing
4. FOLLOW includes $ for start symbol
5. SLR uses FOLLOW for reduce, CLR uses lookahead
6. Synthesized flows up, inherited flows down
7. Left recursion causes infinite loop in recursive descent

---

## 📝 GATE Previous Year Patterns

### Most Frequently Asked Topics
1. **FIRST and FOLLOW Sets** - 2-3 questions/year
2. **LL(1)/LR Parsing Tables** - 1-2 questions/year
3. **Left Recursion Elimination** - 1 question/year
4. **Grammar Ambiguity** - 1 question/year
5. **SDT (Synthesized/Inherited Attributes)** - 1 question/year

### 💡 GATE-Style Practice Problems

**Problem 1 (FIRST & FOLLOW - GATE Pattern):**
```
Grammar:
E → TE'
E' → +TE' | ε
T → FT'
T' → *FT' | ε
F → (E) | id

Calculate FIRST and FOLLOW sets:

FIRST(F) = {(, id}
FIRST(T') = {*, ε}
FIRST(T) = {(, id}
FIRST(E') = {+, ε}
FIRST(E) = {(, id}

FOLLOW(E) = {$, )}
FOLLOW(E') = {$, )}
FOLLOW(T) = {+, $, )}
FOLLOW(T') = {+, $, )}
FOLLOW(F) = {*, +, $, )} ✓
```

**Problem 2 (LL(1) Parsing - GATE Pattern):**
```
Construct LL(1) parsing table for:
S → aABb
A → c | ε
B → d | ε

FIRST(S) = {a}
FIRST(A) = {c, ε}
FIRST(B) = {d, ε}

FOLLOW(S) = {$}
FOLLOW(A) = FIRST(Bb) = {d, b}
FOLLOW(B) = {b}

Parsing Table:
     |  a  |  b  |  c  |  d  |  $
-----|-----|-----|-----|-----|-----
S    |S→aABb|     |     |     |
A    |     |A→ε  |A→c  |A→ε  |
B    |     |B→ε  |     |B→d  |

No conflicts → Grammar is LL(1) ✓
```

**Problem 3 (Left Recursion Elimination - GATE Pattern):**
```
Eliminate left recursion:
E → E + T | E - T | T

Solution:
E → T E'
E' → + T E' | - T E' | ε ✓

General form:
A → Aα₁ | Aα₂ | β₁ | β₂
becomes:
A → β₁A' | β₂A'
A' → α₁A' | α₂A' | ε
```

**Problem 4 (LR(0) Items - GATE Pattern):**
```
Construct LR(0) items for:
S' → S
S → CC
C → cC | d

I0: S' → •S
    S → •CC
    C → •cC
    C → •d

GOTO(I0, S) = I1: S' → S•

GOTO(I0, C) = I2: S → C•C
                  C → •cC
                  C → •d

GOTO(I0, c) = I3: C → c•C
                  C → •cC
                  C → •d

GOTO(I0, d) = I4: C → d•

GOTO(I2, C) = I5: S → CC•
GOTO(I2, c) = I3
GOTO(I2, d) = I4

GOTO(I3, C) = I6: C → cC•
GOTO(I3, c) = I3
GOTO(I3, d) = I4

Total LR(0) states = 7 ✓
```

**Problem 5 (SLR Table Conflict - GATE Pattern):**
```
S → L = R | R
L → *R | id
R → L

Check for SLR conflicts:

I2 contains: S → L•=R and R → L•

For state I2:
- Shift on '=' (for S → L•=R)
- Reduce R → L on FOLLOW(R)

FOLLOW(R) = {=, $}

Conflict! Shift-reduce conflict on '='
This grammar is NOT SLR(1) ✓
```

**Problem 6 (Syntax Directed Definition - GATE Pattern):**
```
SDT for converting infix to postfix:

E → E₁ + T    { E.code = E₁.code || T.code || "+" }
E → T         { E.code = T.code }
T → T₁ * F    { T.code = T₁.code || F.code || "*" }
T → F         { T.code = F.code }
F → (E)       { F.code = E.code }
F → id        { F.code = id.lexval }

Input: a + b * c
Parse tree evaluation:
F.code = "a", T.code = "a", E₁.code = "a"
F.code = "b", T₁.code = "b"
F.code = "c"
T.code = "b" || "c" || "*" = "bc*"
E.code = "a" || "bc*" || "+" = "abc*+"

Output: abc*+ ✓
```

**Problem 7 (Three Address Code - GATE Pattern):**
```
Generate 3AC for: a = b * -c + d / e

TAC:
t1 = -c           (unary minus)
t2 = b * t1
t3 = d / e
t4 = t2 + t3
a = t4

Number of temporaries = 4 ✓
```

**Problem 8 (Basic Blocks - GATE Pattern):**
```
Identify basic blocks:
1. i = 1
2. j = 1
3. t1 = 10 * i
4. t2 = t1 + j
5. t3 = 8 * t2
6. t4 = t3 - 88
7. a[t4] = 0.0
8. j = j + 1
9. if j <= 10 goto 3
10. i = i + 1
11. if i <= 10 goto 2
12. i = 1
...

Leaders: 1, 3, 10, 12
Block B1: statements 1-2
Block B2: statements 3-9
Block B3: statements 10-11
Block B4: statement 12 onwards ✓
```

---

## 📊 Formula Quick Reference Sheet

### Parser Hierarchy
```
LL(1) ⊂ LR(0) ⊂ SLR(1) ⊂ LALR(1) ⊂ LR(1)

Power comparison:
LR(1) > LALR(1) > SLR(1) > LR(0) > LL(1)

LL(1) cannot handle:
- Left recursion
- Left factoring needed
- Ambiguity

LALR(1) = LR(1) states merged by core
Same number of states as SLR(1)
```

### FIRST Set Rules
```
1. FIRST(terminal) = {terminal}
2. FIRST(ε) = {ε}
3. FIRST(A → α) = FIRST(α)
4. If X → Y₁Y₂...Yₖ:
   - Add FIRST(Y₁) - {ε}
   - If ε ∈ FIRST(Y₁), add FIRST(Y₂) - {ε}
   - Continue until non-nullable found
```

### FOLLOW Set Rules
```
1. FOLLOW(Start) includes $
2. If A → αBβ: Add FIRST(β) - {ε} to FOLLOW(B)
3. If A → αB or β derives ε: Add FOLLOW(A) to FOLLOW(B)

Note: ε is NEVER in FOLLOW sets
```

### LR Parsing Actions
```
If [A → α•aβ] in I and GOTO(I, a) = J:
  ACTION[I, a] = shift J

If [A → α•] in I and A ≠ S':
  SLR: ACTION[I, a] = reduce for all a ∈ FOLLOW(A)
  CLR: ACTION[I, a] = reduce for lookahead a only

If [S' → S•] in I:
  ACTION[I, $] = accept
```

### Attribute Evaluation
```
S-attributed (synthesized only):
- Bottom-up evaluation
- Works with LR parsing

L-attributed:
- Left-to-right evaluation
- Inherited from left siblings or parent only
- Works with LL parsing

L-attributed ⊃ S-attributed
```

### Optimization Techniques
```
Local (within basic block):
- Common subexpression elimination
- Dead code elimination
- Constant folding/propagation
- Strength reduction

Global (across blocks):
- Loop invariant code motion
- Induction variable elimination
- Loop unrolling
```

---

## 💡 Additional Important Topics

### Runtime Environments
```
Stack Allocation:
- Activation records on call stack
- Local variables, parameters, return address
- LIFO allocation/deallocation

Heap Allocation:
- Dynamic allocation (malloc/new)
- Garbage collection or manual free
- Fragmentation issues

Static Allocation:
- Global variables
- Static local variables
- Known at compile time
```

### Activation Records
```
Stack Frame Contents (bottom to top):
1. Arguments (passed by caller)
2. Return address
3. Saved frame pointer (old BP)
4. Local variables
5. Temporary values

Frame Pointer (FP/BP): Base of current frame
Stack Pointer (SP): Top of stack
```

### Parameter Passing Mechanisms
```
Call by Value:
- Copy of actual parameter
- Changes don't affect original

Call by Reference:
- Address of actual parameter
- Changes affect original

Call by Value-Result (Copy-in, Copy-out):
- Copy in on call, copy out on return
- Changes copied back at end

Call by Name (Lazy evaluation):
- Expression substituted textually
- Re-evaluated each use
```

### Symbol Table Organization
```
Structures:
- Linear list: O(n) lookup, simple
- Hash table: O(1) average lookup
- Tree: O(log n) lookup, ordered

Scope handling:
- Nested symbol tables
- Stack of tables for block scoping
- Each scope has pointer to enclosing scope
```

### Type Checking
```
Static Type Checking:
- At compile time
- Type errors caught early
- Languages: C, Java, C++

Dynamic Type Checking:
- At runtime
- More flexible but slower
- Languages: Python, JavaScript

Type Synthesis:
- Determine type from subexpressions
- E.g., int + float → float

Type Inference:
- Deduce types without declarations
- E.g., Haskell, ML
```

### Intermediate Representations
```
High-level IR:
- AST (Abstract Syntax Tree)
- Close to source language

Medium-level IR:
- Three-address code
- Control flow graph

Low-level IR:
- Close to machine code
- Register transfer language

SSA (Static Single Assignment):
- Each variable assigned exactly once
- Φ (phi) functions at join points
- Enables many optimizations
```

### Peephole Optimization
```
Small window (peephole) of instructions
Local transformations:

1. Redundant load/store elimination:
   MOV R0, a
   MOV a, R0  ← Remove

2. Algebraic simplification:
   ADD R0, 0  → (nothing)
   MUL R0, 1  → (nothing)
   MUL R0, 2  → SHL R0, 1

3. Jump optimization:
   JUMP L1
   L1: JUMP L2  → JUMP L2

4. Dead code elimination:
   Remove unreachable code
```

### Garbage Collection
```
Reference Counting:
- Count references to each object
- Free when count = 0
- Problem: Cyclic references

Mark and Sweep:
- Mark all reachable objects
- Sweep (free) unmarked objects
- Pauses program execution

Copying Collection:
- Divide heap into two halves
- Copy live objects to other half
- No fragmentation

Generational GC:
- Young objects die quickly
- Collect young generation more often
- Used in Java, .NET
```

### 💡 More GATE-Style Practice Problems

**Problem 9 (Activation Record - GATE Pattern):**
```c
int f(int n) {
    if (n <= 1) return 1;
    return n * f(n-1);
}
// Call f(4)

How many activation records are on the stack at maximum?

Solution:
f(4) calls f(3) calls f(2) calls f(1)
At f(1), stack has: f(4), f(3), f(2), f(1)

Maximum = 4 activation records ✓
```

**Problem 10 (Type Checking - GATE Pattern):**
```
For expression: (a + b) * c[i]
where a: int, b: float, c: array of int, i: int

Find type of expression.

Solution:
1. a + b: int + float = float (coercion)
2. c[i]: int (array indexing)
3. float * int = float (coercion)

Type of expression = float ✓
```

**Problem 11 (Optimization - GATE Pattern):**
```c
Original code:
for (i = 0; i < n; i++) {
    x = y + z;
    a[i] = 6 * i + x;
}

Apply loop optimizations.

Solution:
1. Code motion (y + z is loop invariant):
   x = y + z;
   for (i = 0; i < n; i++) {
       a[i] = 6 * i + x;
   }

2. Strength reduction (replace 6*i with addition):
   x = y + z;
   t = 0;
   for (i = 0; i < n; i++) {
       a[i] = t + x;
       t = t + 6;
   }

Optimizations applied: Loop invariant code motion, Strength reduction ✓
```
