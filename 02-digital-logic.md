# 🔌 Digital Logic - Last Minute Notes

## Quick Navigation
- [Number Systems](#number-systems)
- [Boolean Algebra](#boolean-algebra)
- [Logic Gates](#logic-gates)
- [Minimization Techniques](#minimization-techniques)
- [Combinational Circuits](#combinational-circuits)
- [Sequential Circuits](#sequential-circuits)

---

> **GATE Weightage**: ~3-5% (3-5 marks) | **Expected Questions**: 2-3

---

# Number Systems

## 1. Conversions

### 💡 Quick Conversion Table
| Decimal | Binary | Octal | Hexadecimal |
|---------|--------|-------|-------------|
| 0 | 0000 | 0 | 0 |
| 1 | 0001 | 1 | 1 |
| 2 | 0010 | 2 | 2 |
| 3 | 0011 | 3 | 3 |
| 4 | 0100 | 4 | 4 |
| 5 | 0101 | 5 | 5 |
| 6 | 0110 | 6 | 6 |
| 7 | 0111 | 7 | 7 |
| 8 | 1000 | 10 | 8 |
| 9 | 1001 | 11 | 9 |
| 10 | 1010 | 12 | A |
| 11 | 1011 | 13 | B |
| 12 | 1100 | 14 | C |
| 13 | 1101 | 15 | D |
| 14 | 1110 | 16 | E |
| 15 | 1111 | 17 | F |

### Conversion Tricks
```
Binary → Octal: Group 3 bits from right
Binary → Hex: Group 4 bits from right

Decimal → Binary: Divide by 2, collect remainders
Binary → Decimal: Sum of (bit × 2^position)
```

---

## 2. Signed Number Representations

### 💡 For n-bit representation

| Representation | Range | Example (4-bit) |
|----------------|-------|-----------------|
| **Unsigned** | 0 to 2^n - 1 | 0 to 15 |
| **Sign-Magnitude** | -(2^(n-1) - 1) to +(2^(n-1) - 1) | -7 to +7 |
| **1's Complement** | -(2^(n-1) - 1) to +(2^(n-1) - 1) | -7 to +7 |
| **2's Complement** | -2^(n-1) to +(2^(n-1) - 1) | -8 to +7 |

### 2's Complement (Most Important!)
```
To find 2's complement:
Method 1: Invert all bits + Add 1
Method 2: Keep bits from right until first 1 (including it), then flip rest

Example: -5 in 4 bits
5 = 0101
1's complement = 1010
2's complement = 1011 ✓

Quick trick: -5 = 16 - 5 = 11 = 1011
```

### Important Points
```
• 2's complement: Only ONE representation of zero
• Sign-Magnitude & 1's complement: TWO representations of zero (+0 and -0)
• In 2's complement, MSB = 1 means negative
```

---

# Boolean Algebra

## 1. Basic Laws

### 💡 Fundamental Laws
| Law | OR Form | AND Form |
|-----|---------|----------|
| **Identity** | A + 0 = A | A · 1 = A |
| **Null** | A + 1 = 1 | A · 0 = 0 |
| **Idempotent** | A + A = A | A · A = A |
| **Complement** | A + A' = 1 | A · A' = 0 |
| **Involution** | (A')' = A | (A')' = A |
| **Commutative** | A + B = B + A | A · B = B · A |
| **Associative** | (A+B)+C = A+(B+C) | (A·B)·C = A·(B·C) |
| **Distributive** | A+(B·C) = (A+B)·(A+C) | A·(B+C) = A·B + A·C |

### 💡 De Morgan's Theorems
```
(A + B)' = A' · B'    [Break the bar, change the operator]
(A · B)' = A' + B'
```

### Absorption Laws
```
A + A·B = A
A · (A + B) = A
A + A'·B = A + B
```

---

## 2. Canonical Forms

### Sum of Products (SOP) - Minterms
```
Each minterm: Product of ALL variables (complemented or not)
Example: F(A,B,C) = Σm(1,3,5,7)

m0 = A'B'C'    m4 = AB'C'
m1 = A'B'C     m5 = AB'C
m2 = A'BC'     m6 = ABC'
m3 = A'BC      m7 = ABC
```

### Product of Sums (POS) - Maxterms
```
Each maxterm: Sum of ALL variables (complemented or not)
Example: F(A,B,C) = ΠM(0,2,4,6)

M0 = A+B+C     M4 = A'+B+C
M1 = A+B+C'    M5 = A'+B+C'
M2 = A+B'+C    M6 = A'+B'+C
M3 = A+B'+C'   M7 = A'+B'+C'
```

### Relationship
```
mᵢ = Mᵢ'
If F = Σm(1,3,5) then F' = Σm(0,2,4,6,7) = ΠM(1,3,5)
```

---

# Logic Gates

## 1. Basic Gates

| Gate | Symbol | Expression | Truth for Output=1 |
|------|--------|------------|-------------------|
| **AND** | · | Y = A·B | Both inputs 1 |
| **OR** | + | Y = A+B | At least one input 1 |
| **NOT** | ' | Y = A' | Input is 0 |
| **NAND** | ↑ | Y = (A·B)' | NOT both inputs 1 |
| **NOR** | ↓ | Y = (A+B)' | Both inputs 0 |
| **XOR** | ⊕ | Y = A⊕B = A'B + AB' | Odd number of 1s |
| **XNOR** | ⊙ | Y = (A⊕B)' = AB + A'B' | Even number of 1s (including 0) |

### 💡 Universal Gates
```
NAND and NOR are universal gates - can implement ANY logic function

Using NAND only:
NOT A = A NAND A
A AND B = (A NAND B) NAND (A NAND B)
A OR B = (A NAND A) NAND (B NAND B)

Using NOR only:
NOT A = A NOR A
A OR B = (A NOR B) NOR (A NOR B)
A AND B = (A NOR A) NOR (B NOR B)
```

### XOR Properties
```
A ⊕ 0 = A
A ⊕ 1 = A'
A ⊕ A = 0
A ⊕ A' = 1
A ⊕ B = B ⊕ A          (Commutative)
(A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)  (Associative)
```

---

# Minimization Techniques

## 1. K-Map (Karnaugh Map)

### 💡 K-Map Layout (Gray Code Order!)

**2-Variable K-Map:**
```
      B=0   B=1
A=0    m0    m1
A=1    m2    m3
```

**3-Variable K-Map:**
```
        BC=00  BC=01  BC=11  BC=10
A=0      m0     m1     m3     m2
A=1      m4     m5     m7     m6
```

**4-Variable K-Map:**
```
        CD=00  CD=01  CD=11  CD=10
AB=00    m0     m1     m3     m2
AB=01    m4     m5     m7     m6
AB=11    m12    m13    m15    m14
AB=10    m8     m9     m11    m10
```

### 💡 Grouping Rules
```
1. Groups must be rectangular (powers of 2: 1, 2, 4, 8, 16)
2. Groups can wrap around edges
3. Each cell can be used in multiple groups
4. Make groups as LARGE as possible
5. Use minimum number of groups to cover all 1s
6. Don't-cares (X) can be included if they help make larger groups
```

### Reading the Simplified Expression
```
• For SOP: Group the 1s, write product terms
• For POS: Group the 0s, write sum terms
• Variable = 1 in group → variable uncomplemented
• Variable = 0 in group → variable complemented
• Variable changes (0 and 1) in group → variable eliminated
```

---

## 2. Quine-McCluskey Method

```
Step 1: Convert minterms to binary
Step 2: Group by number of 1s
Step 3: Combine adjacent groups (1-bit difference)
Step 4: Mark combined terms with '-' for differing bit
Step 5: Continue until no more combinations possible
Step 6: Create Prime Implicant Chart
Step 7: Select Essential Prime Implicants
Step 8: Use remaining PIs to cover remaining minterms
```

---

# Combinational Circuits

## 1. Arithmetic Circuits

### Half Adder
```
Inputs: A, B
Outputs: Sum = A ⊕ B
         Carry = A · B
```

### Full Adder
```
Inputs: A, B, Cin
Outputs: Sum = A ⊕ B ⊕ Cin
         Cout = AB + BCin + ACin = AB + Cin(A ⊕ B)
```

### 💡 n-bit Ripple Carry Adder
```
• Uses n Full Adders in cascade
• Delay = 2n gate delays (critical path through all carries)
• Cout of one FA connects to Cin of next
```

### Half Subtractor
```
Inputs: A, B  (A - B)
Outputs: Difference = A ⊕ B
         Borrow = A'B
```

### Full Subtractor
```
Inputs: A, B, Bin
Outputs: Difference = A ⊕ B ⊕ Bin
         Bout = A'B + A'Bin + BBin = A'B + Bin(A ⊕ B)'
```

---

## 2. Multiplexer (MUX)

### 💡 2^n : 1 MUX
```
n select lines → 2^n data inputs → 1 output

4:1 MUX (2 select lines S1, S0):
Y = S1'S0'I0 + S1'S0I1 + S1S0'I2 + S1S0I3

8:1 MUX (3 select lines)
16:1 MUX (4 select lines)
```

### Implementing Functions with MUX
```
For n-variable function, use 2^(n-1):1 MUX

Method:
1. Use (n-1) variables as select lines
2. Last variable appears at data inputs as: 0, 1, A, or A'

Example: F(A,B,C) using 4:1 MUX with A,B as select:
- Make truth table for F
- For each combination of A,B, see if output is 0, 1, C, or C'
```

---

## 3. Demultiplexer (DEMUX)

```
1 data input → n select lines → 2^n outputs

1:4 DEMUX (2 select lines):
Y0 = D·S1'·S0'
Y1 = D·S1'·S0
Y2 = D·S1·S0'
Y3 = D·S1·S0
```

---

## 4. Decoder

### 💡 n:2^n Decoder
```
n inputs → 2^n outputs (exactly ONE output is 1 at a time)

2:4 Decoder outputs:
D0 = A'B' = m0
D1 = A'B  = m1
D2 = AB'  = m2
D3 = AB   = m3

Use: Each output represents a minterm!
```

### Implementing Functions with Decoder
```
For n-variable function, use n:2^n decoder + OR gate

Just OR together the decoder outputs corresponding to minterms!
F(A,B,C) = Σm(1,3,5,7) → F = D1 + D3 + D5 + D7
```

---

## 5. Encoder

### 💡 2^n : n Encoder
```
2^n inputs → n outputs (Priority encoder handles multiple inputs)

8:3 Priority Encoder:
- Highest priority input determines output
- Outputs binary code of highest active input
```

---

## 6. Comparator

### 1-bit Comparator
```
A > B: Y = A·B'
A < B: Y = A'·B
A = B: Y = A⊙B = A'B' + AB = (A ⊕ B)'
```

### n-bit Comparator
```
Compares two n-bit numbers
Outputs: A>B, A<B, A=B
```

---

# Sequential Circuits

## 1. Flip-Flops

### 💡 Flip-Flop Comparison

| FF Type | Excitation | Characteristic Equation | For Q: 0→0 | 0→1 | 1→0 | 1→1 |
|---------|------------|------------------------|------------|-----|-----|-----|
| **SR** | Q+ = S + R'Q | - | S=0,R=X | S=1,R=0 | S=0,R=1 | S=X,R=0 |
| **JK** | Q+ = JQ' + K'Q | - | J=0,K=X | J=1,K=X | J=X,K=1 | J=X,K=0 |
| **D** | Q+ = D | - | D=0 | D=1 | D=0 | D=1 |
| **T** | Q+ = TQ' + T'Q = T⊕Q | - | T=0 | T=1 | T=1 | T=0 |

### Excitation Tables (For State Machine Design)
```
SR FF: S = Q+, R = Q+' (But S·R=0 must hold)
JK FF: J = Q+, K = Q+' (Most flexible)
D FF: D = Q+ (Simplest)
T FF: T = Q ⊕ Q+
```

### FF Conversions
```
SR → JK: Connect S=JQ', R=KQ
SR → D: Connect S=D, R=D'
SR → T: Connect S=TQ', R=TQ
JK → SR: Connect J=S, K=R
JK → D: Connect J=D, K=D'
JK → T: Connect J=K=T
```

---

## 2. Counters

### 💡 Counter Types

| Type | Mod-N | n bits needed | Formula |
|------|-------|---------------|---------|
| Ripple (Async) | 2^n | ⌈log₂N⌉ | Slowest |
| Synchronous | 2^n | ⌈log₂N⌉ | Faster |
| Ring | N | N FFs | Only one 1 circulates |
| Johnson | 2N | N FFs | 1s enter, then 0s |

### Mod-N Counter Design
```
Number of FFs needed = ⌈log₂N⌉

For Mod-6 counter: need 3 FFs (since 2²=4 < 6, 2³=8 ≥ 6)

Method for Mod-N (if N ≠ 2^k):
1. Design for Mod-2^k counter (k = ⌈log₂N⌉)
2. Detect state N and force reset to 0
```

### Ripple Counter Timing
```
Maximum frequency = 1 / (n × propagation delay)
Where n = number of flip-flops
```

---

## 3. Registers

### 💡 Shift Register Types
| Type | Operation |
|------|-----------|
| **SISO** | Serial In, Serial Out |
| **SIPO** | Serial In, Parallel Out |
| **PISO** | Parallel In, Serial Out |
| **PIPO** | Parallel In, Parallel Out |

### Shift Register Applications
```
• Serial data transfer
• Time delay (n clock cycles for n-bit register)
• Conversion between serial and parallel
• Ring counter / Johnson counter
• Sequence generator
```

---

## 4. Finite State Machines (FSM)

### Moore vs Mealy

| Aspect | Moore | Mealy |
|--------|-------|-------|
| **Output depends on** | Current state only | Current state + Current input |
| **Output changes** | With state change (clock edge) | Immediately with input |
| **Number of states** | More states | Fewer states |
| **Output timing** | Synchronized with clock | Asynchronous with input |

### 💡 State Machine Design Steps
```
1. Draw State Diagram
2. Create State Table
3. State Assignment (binary codes)
4. Derive FF Input Equations (using K-map)
5. Derive Output Equations
6. Draw Circuit
```

---

## Quick Memory Tricks 🧠

1. **2's Complement**: "Flip and add 1"
2. **De Morgan**: "Break the bar, change the sign"
3. **K-Map order**: "Gray code - only 1 bit changes"
4. **XOR**: "True when inputs are different"
5. **NAND/NOR Universal**: "NANDs for AND-OR, NORs for OR-AND"
6. **MUX to implement function**: "Select lines = (n-1) variables"
7. **Decoder + OR**: "Each output is a minterm"

---

## Common Mistakes to Avoid ⚠️

1. Wrong K-map adjacent cell order (must be Gray code!)
2. Forgetting K-map wraps around (top-bottom, left-right)
3. Confusing SR FF invalid state (S=R=1) with JK toggle (J=K=1)
4. Wrong direction in ripple counter timing analysis
5. Forgetting that Moore outputs are delayed by 1 clock vs Mealy
6. Mixing up encoder and decoder
7. 2's complement range asymmetry (-8 to +7 for 4 bits)

---

## 📝 GATE Previous Year Patterns

### Most Frequently Asked Topics
1. **K-Map Minimization** - 1-2 questions/year
2. **Number System Conversions** - 1 question/year
3. **Flip-Flop Excitation Tables** - 1 question/year
4. **Counter Design** - 1 question/year
5. **MUX/Decoder Implementation** - 1 question/year

### 💡 GATE-Style Practice Problems

**Problem 1 (K-Map - GATE Pattern):**
```
Minimize F(A,B,C,D) = Σm(0,1,2,5,8,9,10) with don't cares d(3,11,15)

Solution:
Draw 4-variable K-map:
        CD=00  CD=01  CD=11  CD=10
AB=00     1      1      X      1
AB=01     0      1      0      0
AB=11     0      0      X      0
AB=10     1      1      X      1

Grouping:
- Group m0,m1,m8,m9 with d3,d11: B'D' (4 cells vertically)
- Group m0,m2,m8,m10: C'D' (4 corner cells)
- Group m1,m5: A'B'D

F = B'D' + C'D' + A'B'D
Or simplified: F = B'C' + B'D' + A'B'D ✓
```

**Problem 2 (Counter - GATE Pattern):**
```
Design a Mod-6 synchronous counter using JK flip-flops.

Solution:
States: 000 → 001 → 010 → 011 → 100 → 101 → 000
Present  Next   J2 K2  J1 K1  J0 K0
Q2Q1Q0  Q2Q1Q0
000     001     0  X   0  X   1  X
001     010     0  X   1  X   X  1
010     011     0  X   X  0   1  X
011     100     1  X   X  1   X  1
100     101     X  0   0  X   1  X
101     000     X  1   0  X   X  1

From K-maps:
J2 = Q1Q0, K2 = Q0
J1 = Q2'Q0, K1 = Q0
J0 = 1, K0 = 1
```

**Problem 3 (MUX Implementation - GATE Pattern):**
```
Implement F(A,B,C) = Σm(1,2,6,7) using a 4:1 MUX with A,B as select lines.

Solution:
Create truth table with A,B as select, find C input:
A=0,B=0: m0=0, m1=1 → output depends on C → Input = C
A=0,B=1: m2=1, m3=0 → output depends on C' → Input = C'
A=1,B=0: m4=0, m5=0 → output = 0 → Input = 0
A=1,B=1: m6=1, m7=1 → output = 1 → Input = 1

MUX inputs: I0=C, I1=C', I2=0, I3=1 ✓
```

**Problem 4 (Number System - GATE Pattern):**
```
What is the 2's complement representation of -43 in 8 bits?

Solution:
43 in binary = 00101011
1's complement = 11010100
2's complement = 11010101 ✓

Verification: 256 - 43 = 213 = 11010101
```

**Problem 5 (Sequential Circuit - GATE Pattern):**
```
A Moore machine has input X and output Z. Z=1 if input sequence 
ends in "101". Find minimum number of states.

Solution:
States needed to remember:
- S0: Initial/no relevant history
- S1: Seen "1"
- S2: Seen "10"
- S3: Seen "101" (output Z=1)

Minimum states = 4

For Mealy machine, same problem needs only 3 states.
```

---

## 📊 Formula Quick Reference Sheet

### Number Systems
```
2's complement of N (n bits): 2^n - N
Range of 2's complement: -2^(n-1) to 2^(n-1) - 1
Range of unsigned: 0 to 2^n - 1
```

### Boolean Algebra
```
Absorption: A + AB = A, A(A+B) = A
Consensus: AB + A'C + BC = AB + A'C
De Morgan: (A+B)' = A'B', (AB)' = A'+B'
```

### K-Map Grouping
```
Group of 1: 4 variables remain
Group of 2: 3 variables remain  
Group of 4: 2 variables remain
Group of 8: 1 variable remains
Group of 16: 0 variables (constant 1 or 0)
```

### Counters
```
Mod-N counter FFs needed: ⌈log₂N⌉
Ring counter: N states needs N FFs
Johnson counter: 2N states needs N FFs
Max frequency (ripple): f_max = 1/(n × t_propagation)
```

### Flip-Flop Conversions
```
D = Q+ (next state)
T = Q ⊕ Q+ (toggle when different)
JK: J = Q+, K = Q+'  (most flexible)
```

### Gate Counts
```
2:1 MUX gates: 3 (2 AND, 1 OR) + 1 NOT = 4
4:1 MUX: Uses 3 × 2:1 MUX
Full Adder: 2 XOR + 2 AND + 1 OR (for sum and carry)
```

---

## 💡 Additional Important Topics

### Hazards in Combinational Circuits
```
Static Hazard:
- Static-1 hazard: Output should be 1, momentarily goes to 0
- Static-0 hazard: Output should be 0, momentarily goes to 1
- Cause: Different path delays for signals

Detection: Check K-map for adjacent 1s not covered by same group
Solution: Add redundant terms to cover adjacent transitions

Dynamic Hazard:
- Output changes multiple times before settling
- Occurs in multi-level circuits
- Solution: Reduce to two-level implementation
```

### Carry Lookahead Adder (CLA)
```
Generate (G): Gᵢ = Aᵢ · Bᵢ
Propagate (P): Pᵢ = Aᵢ ⊕ Bᵢ

Carry equations:
C₁ = G₀ + P₀C₀
C₂ = G₁ + P₁G₀ + P₁P₀C₀
C₃ = G₂ + P₂G₁ + P₂P₁G₀ + P₂P₁P₀C₀
C₄ = G₃ + P₃G₂ + P₃P₂G₁ + P₃P₂P₁G₀ + P₃P₂P₁P₀C₀

Advantages:
- O(1) delay for carry generation (vs O(n) for ripple)
- Fast addition at cost of more hardware
```

### Binary Multiplier
```
For n-bit × n-bit multiplication:
- Produces 2n-bit result
- Uses array of AND gates and adders
- Partial products added using adder array

Time: O(n) with array multiplier
Gate count: n² AND gates + n(n-1) full adders
```

### BCD (Binary Coded Decimal)
```
Each decimal digit represented by 4 bits
Valid: 0000 (0) to 1001 (9)
Invalid: 1010 to 1111

BCD Addition:
1. Add as binary
2. If sum > 9 or carry out, add 0110 (6)

Example: 7 + 8 = 0111 + 1000 = 1111 (15 in binary)
15 > 9, so add 6: 1111 + 0110 = 10101 = 15 in BCD (0001 0101)
```

### Gray Code
```
Advantage: Only one bit changes between adjacent codes
Conversion Binary to Gray:
G[n] = B[n] (MSB same)
G[i] = B[i+1] ⊕ B[i]

Conversion Gray to Binary:
B[n] = G[n]
B[i] = B[i+1] ⊕ G[i]

Used in: K-maps, shaft encoders, error reduction
```

### ASM Charts (Algorithmic State Machines)
```
Components:
- State box (rectangle): Contains state name and outputs
- Decision box (diamond): Binary decision point
- Conditional output box (oval): Output dependent on input

Equivalent to: State diagram with Moore/Mealy outputs
Used for: Designing sequential control units
```

### Programmable Logic Devices
```
PLA (Programmable Logic Array):
- Programmable AND array + Programmable OR array
- Most flexible, more expensive

PAL (Programmable Array Logic):
- Programmable AND array + Fixed OR array
- Less flexible, cheaper

ROM as Logic Device:
- Fixed AND array (decoder) + Programmable OR array
- Can implement any function

FPGA (Field Programmable Gate Array):
- Configurable logic blocks
- Programmable interconnects
- Used for complex digital systems
```

### Timing Diagrams
```
Important parameters:
- Setup time (tₛ): Input must be stable BEFORE clock edge
- Hold time (tₕ): Input must be stable AFTER clock edge
- Propagation delay (tₚ): Clock to output change

Maximum clock frequency:
f_max = 1 / (tₚ + t_combinational + tₛ)
```

### 💡 More GATE-Style Practice Problems

**Problem 6 (CLA - GATE Pattern):**
```
For a 4-bit Carry Lookahead Adder, if G₀=0, G₁=1, G₂=0, G₃=1
and P₀=1, P₁=0, P₂=1, P₃=1, with C₀=1, find C₄.

Solution:
C₄ = G₃ + P₃G₂ + P₃P₂G₁ + P₃P₂P₁G₀ + P₃P₂P₁P₀C₀
   = 1 + 1·0 + 1·1·1 + 1·1·0·0 + 1·1·0·1·1
   = 1 + 0 + 1 + 0 + 0
   = 1 ✓
```

**Problem 7 (Hazard Detection - GATE Pattern):**
```
Detect static hazards in F = AB + BC

K-map for F:
      C=0  C=1
AB=00   0    0
AB=01   0    1
AB=11   1    1
AB=10   1    0

Groups: AB (covers m6, m7) and BC (covers m3, m7)
m7 is covered by both groups ✓

Static-1 hazard exists when transitioning between AB=11,C=0 
and AB=01,C=1 (both give F=1 but through different paths)

Fix: Add redundant term AC to cover the hazard
F = AB + BC + AC ✓
```

**Problem 8 (BCD Subtraction - GATE Pattern):**
```
Subtract 37 from 85 using 10's complement (BCD).

Solution:
10's complement of 37 = 99 - 37 + 1 = 63

Add: 85 + 63 = 148
Drop the carry (1): Result = 48 ✓

Verification: 85 - 37 = 48 ✓
```
