# 🧮 General Aptitude - Last Minute Notes

## Quick Navigation
- [Quantitative Aptitude](#quantitative-aptitude)
- [Verbal Ability](#verbal-ability)
- [Logical Reasoning](#logical-reasoning)

---

> **GATE Weightage**: ~15% (15 marks) | **Expected Questions**: 10 (5×1 mark + 5×2 marks)

---

# Quantitative Aptitude

## 1. Number System

### 💡 Divisibility Rules
| Divisor | Rule |
|---------|------|
| 2 | Last digit even |
| 3 | Sum of digits divisible by 3 |
| 4 | Last 2 digits divisible by 4 |
| 5 | Last digit 0 or 5 |
| 6 | Divisible by both 2 and 3 |
| 8 | Last 3 digits divisible by 8 |
| 9 | Sum of digits divisible by 9 |
| 10 | Last digit 0 |
| 11 | (Sum of odd positions) - (Sum of even positions) divisible by 11 |

### HCF and LCM
```
HCF × LCM = Product of two numbers

For n numbers:
LCM = Product of highest powers of all prime factors
HCF = Product of lowest powers of common prime factors

For fractions:
HCF = HCF of numerators / LCM of denominators
LCM = LCM of numerators / HCF of denominators
```

---

## 2. Percentages

### 💡 Key Formulas
```
Percentage = (Part / Whole) × 100

Percentage increase = [(New - Old) / Old] × 100
Percentage decrease = [(Old - New) / Old] × 100

If X% increase followed by Y% decrease:
Net change = X - Y - (XY/100) %

If both increase or both decrease by X%:
Net change = X + Y + (XY/100) % (sign based on direction)
```

### 💡 Percentage ↔ Fraction Conversions
| Percentage | Fraction |
|------------|----------|
| 10% | 1/10 |
| 12.5% | 1/8 |
| 16.67% | 1/6 |
| 20% | 1/5 |
| 25% | 1/4 |
| 33.33% | 1/3 |
| 50% | 1/2 |
| 66.67% | 2/3 |
| 75% | 3/4 |

---

## 3. Profit and Loss

### 💡 Key Formulas
```
Profit = SP - CP
Loss = CP - SP

Profit % = (Profit / CP) × 100
Loss % = (Loss / CP) × 100

SP = CP × (100 + Profit%) / 100
SP = CP × (100 - Loss%) / 100

Marked Price: MP = CP × (100 + Markup%) / 100
Discount: Discount = (Discount% × MP) / 100
SP = MP - Discount
```

### 💡 Two Articles Same SP
```
If one gives x% profit and other x% loss:
Net Loss = (x²/100) %
```

---

## 4. Simple and Compound Interest

### 💡 Simple Interest
```
SI = (P × R × T) / 100

A = P + SI = P(1 + RT/100)

Where:
P = Principal
R = Rate per annum
T = Time in years
A = Amount
```

### 💡 Compound Interest
```
A = P(1 + R/100)^n

CI = A - P = P[(1 + R/100)^n - 1]

For different compounding:
Half-yearly: R → R/2, n → 2n
Quarterly: R → R/4, n → 4n
```

### 💡 SI vs CI Difference
```
For 2 years:
CI - SI = P(R/100)²

For 3 years:
CI - SI = P(R/100)²(3 + R/100)
```

---

## 5. Ratio and Proportion

### 💡 Key Concepts
```
a:b = c:d (proportion)
⟹ a × d = b × c (cross multiplication)

Componendo: (a+b)/b = (c+d)/d
Dividendo: (a-b)/b = (c-d)/d

If a:b = c:d:
Componendo-Dividendo: (a+b)/(a-b) = (c+d)/(c-d)
```

### 💡 Mixture Problems
```
If two quantities with costs C₁ and C₂ mixed to get mean cost Cₘ:
Quantity ratio = (C₂ - Cₘ) : (Cₘ - C₁)  (Alligation rule)

Replacement formula:
After n replacements: Remaining = V × (1 - R/V)^n
Where V = vessel capacity, R = quantity replaced each time
```

---

## 6. Time and Work

### 💡 Key Formulas
```
If A can do work in x days:
A's 1 day work = 1/x

Combined work:
If A does in x days, B in y days:
Together: 1/x + 1/y = (x+y)/xy
Days together = xy/(x+y)

If A is x times as efficient as B:
Time ratio = 1:x
Work ratio = x:1
```

### 💡 Work and Wages
```
Wages are proportional to work done
If total wage is W:
A's wage = (A's work / Total work) × W
```

---

## 7. Time, Speed, Distance

### 💡 Basic Formulas
```
Speed = Distance / Time
Distance = Speed × Time
Time = Distance / Speed

Average Speed (for same distance at different speeds):
Avg Speed = 2 × S₁ × S₂ / (S₁ + S₂)

Relative Speed:
Same direction: |S₁ - S₂|
Opposite direction: S₁ + S₂
```

### 💡 Unit Conversions
```
km/hr to m/s: Multiply by 5/18
m/s to km/hr: Multiply by 18/5
```

### 💡 Trains
```
Time to cross pole/person = Length of train / Speed
Time to cross platform = (Length of train + Platform) / Speed
Time to cross another train (same direction) = (L₁ + L₂) / |S₁ - S₂|
Time to cross another train (opposite) = (L₁ + L₂) / (S₁ + S₂)
```

### 💡 Boats and Streams
```
Downstream speed = Boat speed + Stream speed
Upstream speed = Boat speed - Stream speed

Boat speed = (Downstream + Upstream) / 2
Stream speed = (Downstream - Upstream) / 2
```

---

## 8. Permutations and Combinations

### 💡 Formulas
```
Factorial: n! = n × (n-1) × (n-2) × ... × 1
0! = 1

Permutation (order matters):
P(n,r) = n! / (n-r)!

Combination (order doesn't matter):
C(n,r) = n! / [r!(n-r)!] = P(n,r) / r!

Properties:
C(n,r) = C(n, n-r)
C(n,0) = C(n,n) = 1
C(n,1) = n
```

### 💡 Common Arrangements
```
Circular arrangement: (n-1)!
Arrangement with repetition: n^r
Distribution in groups: n! / (k₁! × k₂! × ...)
```

---

## 9. Probability

### 💡 Basic Probability
```
P(E) = Favorable outcomes / Total outcomes
0 ≤ P(E) ≤ 1
P(E) + P(E') = 1

Addition rule:
P(A ∪ B) = P(A) + P(B) - P(A ∩ B)
For mutually exclusive: P(A ∪ B) = P(A) + P(B)

Multiplication rule:
P(A ∩ B) = P(A) × P(B|A)
For independent: P(A ∩ B) = P(A) × P(B)
```

### 💡 Common Probabilities
```
Coin: P(Head) = P(Tail) = 1/2
Die: P(any number) = 1/6
Card: P(any specific card) = 1/52
     P(any suit) = 13/52 = 1/4
     P(face card) = 12/52 = 3/13
```

---

## 10. Geometry

### 💡 Triangles
```
Area = (1/2) × base × height
     = √[s(s-a)(s-b)(s-c)]  (Heron's formula, s = (a+b+c)/2)
     = (1/2) × a × b × sin(C)

For right triangle:
Area = (1/2) × base × perpendicular
Pythagorean: a² + b² = c² (c = hypotenuse)

Common right triangles:
3-4-5, 5-12-13, 7-24-25, 8-15-17, 9-40-41

Equilateral triangle (side a):
Area = (√3/4) × a²
Height = (√3/2) × a
```

### 💡 Circles
```
Circumference = 2πr
Area = πr²

Arc length = (θ/360) × 2πr = (θ/2) × r (θ in radians)
Sector area = (θ/360) × πr² = (1/2) × r² × θ (θ in radians)
```

### 💡 Quadrilaterals
```
Square (side a):
Area = a², Diagonal = a√2

Rectangle (l × b):
Area = l × b, Diagonal = √(l² + b²)

Parallelogram:
Area = base × height

Trapezium (parallel sides a, b; height h):
Area = (1/2) × (a + b) × h

Rhombus (diagonals d₁, d₂):
Area = (1/2) × d₁ × d₂
```

### 💡 3D Shapes
```
Cube (side a):
Volume = a³
Surface area = 6a²
Diagonal = a√3

Cuboid (l × b × h):
Volume = l × b × h
Surface area = 2(lb + bh + hl)
Diagonal = √(l² + b² + h²)

Cylinder (radius r, height h):
Volume = πr²h
Curved surface = 2πrh
Total surface = 2πr(r + h)

Cone (radius r, height h, slant l):
Volume = (1/3)πr²h
Curved surface = πrl
l = √(r² + h²)

Sphere (radius r):
Volume = (4/3)πr³
Surface area = 4πr²
```

---

# Verbal Ability

## 1. Vocabulary

### 💡 Common Synonyms
| Word | Synonym |
|------|---------|
| Abandon | Desert, Forsake |
| Abundant | Plentiful, Copious |
| Adequate | Sufficient, Enough |
| Adversity | Hardship, Misfortune |
| Ambiguous | Unclear, Vague |
| Benevolent | Kind, Charitable |
| Candid | Frank, Honest |
| Diligent | Hardworking, Industrious |
| Enhance | Improve, Augment |
| Inevitable | Unavoidable, Certain |

### 💡 Common Antonyms
| Word | Antonym |
|------|---------|
| Abstract | Concrete |
| Accept | Reject |
| Abundant | Scarce |
| Advance | Retreat |
| Ancient | Modern |
| Artificial | Natural |
| Brave | Cowardly |
| Complex | Simple |
| Flexible | Rigid |
| Temporary | Permanent |

---

## 2. Grammar

### 💡 Common Errors
```
Subject-Verb Agreement:
• Collective nouns take singular verb
• "Either...or", "Neither...nor" - verb agrees with nearest subject
• "Along with", "as well as" - verb agrees with first subject

Pronoun Errors:
• Pronoun must agree with antecedent in number
• Use "whom" for objects, "who" for subjects

Tenses:
• Don't mix tenses unless necessary
• Present perfect for actions continuing to present
• Past perfect for action before another past action
```

### 💡 Commonly Confused Words
| Words | Difference |
|-------|------------|
| Affect / Effect | Affect = verb; Effect = noun |
| Accept / Except | Accept = receive; Except = exclude |
| Principal / Principle | Principal = main/person; Principle = rule |
| Stationary / Stationery | Stationary = not moving; Stationery = paper |
| Their / There / They're | Their = possession; There = place; They're = they are |
| Its / It's | Its = possession; It's = it is |

---

## 3. Reading Comprehension

### 💡 Tips
```
1. Skim the passage first
2. Read questions before detailed reading
3. Look for keywords in passage
4. Eliminate obviously wrong answers
5. Don't make assumptions beyond the text
6. Pay attention to tone and main idea
```

---

## 4. Sentence Correction

### 💡 Common Issues
```
1. Subject-verb agreement
2. Pronoun reference
3. Parallelism (similar structures)
4. Modifier placement
5. Tense consistency
6. Active vs passive voice
7. Redundancy
```

---

# Logical Reasoning

## 1. Blood Relations

### 💡 Key Relationships
```
Father's/Mother's father → Grandfather
Father's/Mother's mother → Grandmother
Father's brother → Uncle
Father's sister → Aunt
Mother's brother → Maternal uncle
Mother's sister → Aunt
Brother's/Sister's son → Nephew
Brother's/Sister's daughter → Niece
```

### 💡 Tips
```
• Draw family tree
• Use + for male, - for female
• Identify the relationship step by step
• Be careful with spouse relationships
```

---

## 2. Direction Sense

### 💡 Direction Reference
```
        North
          ↑
West  ←   +   →  East
          ↓
        South

Clockwise: N → E → S → W
Counter-clockwise: N → W → S → E

Right turn: 90° clockwise
Left turn: 90° counter-clockwise
About turn: 180°
```

### 💡 Tips
```
• Draw diagram
• Start from origin
• Track all turns carefully
• Use Pythagorean theorem for shortest distance
```

---

## 3. Coding-Decoding

### 💡 Types
```
Letter Coding:
• Letter shifting (A+1=B, A+2=C)
• Reverse alphabet (A=Z, B=Y)
• Position-based coding

Number Coding:
• Position of letter (A=1, B=2)
• Sum of positions
• Mathematical operations

Mixed Coding:
• Combination of above
```

---

## 4. Syllogisms

### 💡 Basic Forms
```
All A are B
Some A are B
No A is B
Some A are not B
```

### 💡 Valid Conclusions
```
All A are B + All B are C → All A are C
All A are B + Some B are C → Some A are C (NOT valid)
All A are B + No B is C → No A is C
Some A are B + All B are C → Some A are C
Some A are B + No B is C → Some A are not C
```

### 💡 Tips
```
• Use Venn diagrams
• Mark definite regions
• Check if conclusion is DEFINITELY true
• "Some" includes possibility of "All"
```

---

## 5. Data Interpretation

### 💡 Types
```
Bar Graph: Compare categories
Line Graph: Show trends over time
Pie Chart: Show proportions (total = 360°)
Table: Precise numerical data
```

### 💡 Common Calculations
```
Percentage change = [(New - Old) / Old] × 100
Ratio = Value₁ : Value₂
Average = Sum / Count
Weighted Average = Σ(value × weight) / Σweights
```

### 💡 Pie Chart Formula
```
Central angle = (Value / Total) × 360°
Value = (Central angle / 360°) × Total
```

---

## 6. Series

### 💡 Number Series Patterns
```
• Arithmetic: Add/subtract constant (2, 5, 8, 11...)
• Geometric: Multiply/divide constant (2, 6, 18, 54...)
• Fibonacci: Sum of previous two (1, 1, 2, 3, 5, 8...)
• Squares: n² (1, 4, 9, 16, 25...)
• Cubes: n³ (1, 8, 27, 64...)
• Alternating: Different patterns for odd/even positions
• Mixed: Combination of operations
```

### 💡 Letter Series Patterns
```
• Position increment (A, C, E, G → +2 positions)
• Reverse order
• Vowel/consonant patterns
```

---

## Quick Memory Tricks 🧠

1. **Percentage to fraction**: 12.5% = 1/8, 16.67% = 1/6
2. **Speed conversion**: km/hr × 5/18 = m/s
3. **CI formula**: Amount = P(1 + r/100)^n
4. **Trains crossing**: Add lengths, speed depends on direction
5. **Combinations**: C(n,r) = C(n, n-r)
6. **Circle area**: πr² (pi r squared)
7. **Volume of sphere**: (4/3)πr³

---

## 💡 Quick Calculation Tips

```
Multiplication by 11: 25 × 11 = 2(2+5)5 = 275
Squaring numbers ending in 5: 35² = (3×4)|25 = 1225
Percentage of: 15% of 80 = 80% of 15 = 12

Approximations:
√2 ≈ 1.414
√3 ≈ 1.732
√5 ≈ 2.236
π ≈ 3.14 or 22/7
```

---

## Common Mistakes to Avoid ⚠️

1. Confusing percentage increase with percentage of
2. Wrong unit conversion (km/hr vs m/s)
3. Missing special cases in probability (replacement, order)
4. Rushing through reading comprehension
5. Assuming information not given in passage
6. Drawing family tree incorrectly
7. Confusing rows/columns in tables
8. Not checking all options in syllogisms

---

## 📝 GATE Previous Year Patterns

### Most Frequently Asked Topics
1. **Reading Comprehension** - 1-2 questions/year
2. **Data Interpretation** - 1-2 questions/year
3. **Percentages/Profit-Loss** - 1-2 questions/year
4. **Time-Speed-Distance** - 1 question/year
5. **Probability** - 1 question/year
6. **Logical Reasoning** - 2-3 questions/year
7. **Verbal Ability (Grammar/Vocab)** - 2-3 questions/year

### 💡 GATE-Style Practice Problems

**Problem 1 (Percentage - GATE Pattern):**
```
A shopkeeper marks up goods by 40% and then offers 20% discount.
What is the profit percentage?

Solution:
Let CP = 100
MP = 100 + 40% = 140
SP = 140 - 20% of 140 = 140 - 28 = 112

Profit = 112 - 100 = 12
Profit % = 12% ✓

Formula: Net effect = (40 - 20 - (40×20)/100)% = (40-20-8)% = 12%
```

**Problem 2 (Time & Work - GATE Pattern):**
```
A can complete work in 12 days, B in 18 days.
They work together for 4 days, then A leaves.
How many more days will B take to finish?

Solution:
A's 1 day work = 1/12
B's 1 day work = 1/18
Combined = 1/12 + 1/18 = 5/36 per day

Work done in 4 days = 4 × 5/36 = 20/36 = 5/9
Remaining work = 1 - 5/9 = 4/9

Time for B to complete 4/9 = (4/9) / (1/18) = 4/9 × 18 = 8 days ✓
```

**Problem 3 (Probability - GATE Pattern):**
```
Three unbiased coins are tossed. What is the probability of 
getting at least 2 heads?

Solution:
Total outcomes = 2³ = 8
Favorable outcomes:
- Exactly 2 heads: HHT, HTH, THH = 3
- Exactly 3 heads: HHH = 1
Total favorable = 4

P(at least 2 heads) = 4/8 = 1/2 ✓

Using formula: P(X≥2) = C(3,2)(1/2)² + C(3,3)(1/2)³
= 3×(1/4)×(1/2) + 1×(1/8) = 3/8 + 1/8 = 4/8 = 1/2
```

**Problem 4 (Mixture - GATE Pattern):**
```
A vessel contains 60 liters of milk. 12 liters is removed 
and replaced with water. This is done 3 times.
How much milk remains?

Solution:
After each operation, milk remaining = V × (1 - R/V)

After 3 operations:
Milk = 60 × (1 - 12/60)³
= 60 × (48/60)³
= 60 × (4/5)³
= 60 × 64/125
= 30.72 liters ✓
```

**Problem 5 (Time Speed Distance - GATE Pattern):**
```
A train 150m long passes a platform 350m long in 25 seconds.
Find the speed of the train.

Solution:
Total distance = Train length + Platform length
= 150 + 350 = 500 m

Speed = Distance / Time = 500 / 25 = 20 m/s

In km/hr = 20 × 18/5 = 72 km/hr ✓
```

**Problem 6 (Data Interpretation - GATE Pattern):**
```
Year    Sales (in crores)
2018    120
2019    150
2020    135
2021    180
2022    200

What is the CAGR (Compound Annual Growth Rate) from 2018 to 2022?

Solution:
CAGR = (Final/Initial)^(1/n) - 1
= (200/120)^(1/4) - 1
= (1.667)^0.25 - 1
= 1.136 - 1
= 0.136 = 13.6% ✓
```

**Problem 7 (Logical Reasoning - GATE Pattern):**
```
Statements:
1. All doctors are engineers
2. Some engineers are managers

Conclusions:
I. Some doctors are managers
II. Some managers are engineers

Solution:
Using Venn diagrams:
- All doctors inside engineers (D ⊂ E)
- Some engineers overlap with managers (E ∩ M ≠ ∅)

Conclusion I: Cannot be definitively concluded
(Doctors may or may not be in the engineer-manager overlap)

Conclusion II: Definitely true
(Given directly in statement 2)

Answer: Only II follows ✓
```

**Problem 8 (Coding-Decoding - GATE Pattern):**
```
If FRIEND = HUMJTK, then ENEMY = ?

Solution:
Analyze pattern:
F(6) → H(8): +2
R(18) → U(21): +3
I(9) → M(13): +4
E(5) → J(10): +5
N(14) → T(20): +6
D(4) → K(11): +7

Pattern: Each letter shifted by increasing amounts (+2, +3, +4, +5, +6, +7)

For ENEMY:
E(5) + 2 = G(7)
N(14) + 3 = Q(17)
E(5) + 4 = I(9)
M(13) + 5 = R(18)
Y(25) + 6 = E(5) [wrapping: 25+6=31, 31-26=5]

Answer: GQIRE ✓
```

**Problem 9 (Verbal - Sentence Correction - GATE Pattern):**
```
Identify the error:
"Neither the teacher nor the students was present."

Error: Subject-verb agreement
Rule: With "neither...nor", verb agrees with the NEAREST subject.
Nearest subject: "students" (plural) → verb should be "were"

Correct: "Neither the teacher nor the students were present." ✓
```

**Problem 10 (Critical Reasoning - GATE Pattern):**
```
Statement: "Regular exercise leads to better health."

Which of the following, if true, most weakens the argument?

A) Some people who exercise regularly are healthy
B) People who don't exercise can also be healthy
C) Exercise requires time and discipline
D) Some exercises can cause injuries

Analysis:
A) Supports the argument
B) Shows exercise is not necessary, but doesn't weaken causation
C) Irrelevant to the claim
D) Weakens by showing exercise can have negative effects

Answer: D ✓
```

---

## 📊 Formula Quick Reference Sheet

### Speed & Conversion
```
Speed = Distance / Time
km/hr × 5/18 = m/s
m/s × 18/5 = km/hr

Relative speed (same direction): |S1 - S2|
Relative speed (opposite): S1 + S2
```

### Percentages
```
% increase = (New - Old) / Old × 100
% decrease = (Old - New) / Old × 100

Successive changes: a% then b% → a + b + ab/100
If same % up then down: Net loss = x²/100 %
```

### Interest
```
Simple Interest: SI = PRT/100
Compound Interest: A = P(1 + R/100)^n

CI - SI (2 years) = P(R/100)²
CI - SI (3 years) = P(R/100)²(3 + R/100)
```

### Work
```
1/A + 1/B = 1/Total (for work rates)
If A is x times efficient as B: Time ratio = 1:x

Work = Rate × Time
A does 1/x work per day → completes in x days
```

### Probability
```
P(A∪B) = P(A) + P(B) - P(A∩B)
P(A∩B) = P(A) × P(B) [if independent]
P(A|B) = P(A∩B) / P(B)

n(E) = ways favorable
n(S) = total outcomes
P(E) = n(E) / n(S)
```

### Geometry
```
Triangle: Area = ½ × base × height = ½ × a × b × sin(C)
Circle: Area = πr², Circumference = 2πr
Cylinder: Volume = πr²h, Surface = 2πr(r+h)
Sphere: Volume = (4/3)πr³, Surface = 4πr²
```

### Data Interpretation
```
CAGR = (Final/Initial)^(1/n) - 1
Average = Sum / Count
Percentage share = (Part/Whole) × 100
Pie chart: Angle = (Value/Total) × 360°
```

---

## 💡 Quick Tips for GATE Aptitude

### Time Management
```
1-mark questions: ~1 minute each
2-mark questions: ~2-3 minutes each
Total time for aptitude: 15-20 minutes max
```

### Strategy
```
1. Attempt aptitude first (confidence boost)
2. Reading comprehension: Read questions first
3. Data interpretation: Check options before calculating
4. Eliminate wrong options when stuck
5. Never leave NAT questions blank
```

### Common Traps
```
- "At least one" vs "Exactly one"
- "More than" vs "Not less than"  
- Percentage OF vs Percentage MORE THAN
- Average vs Weighted Average
- Include/Exclude boundary values
```

---

## 💡 Additional Important Topics

### Analytical Reasoning
```
Types:
1. Arrangements (Linear/Circular)
2. Grouping/Selections
3. Matching/Mapping
4. Scheduling
5. Ordering

Strategy:
1. Read all conditions carefully
2. Make a diagram or table
3. Start with most restrictive condition
4. Use elimination for MCQs
```

### Verbal Reasoning
```
Sentence Completion:
- Look for context clues
- Check for parallel structure
- Consider tone of passage

Para Jumbles:
- Find the opening sentence (introduces topic)
- Look for pronouns and their antecedents
- Identify connecting words (however, moreover, therefore)
- Find closing sentence (conclusion/summary)
```

### Critical Reasoning
```
Strengthening Arguments:
- Find assumption and support it
- Provide additional evidence

Weakening Arguments:
- Attack the assumption
- Provide counter-evidence

Identify the Assumption:
- Find the gap between premise and conclusion
- The assumption bridges this gap
```

### Calendar Problems
```
Odd days in a year:
- Normal year: 365 = 52×7 + 1 → 1 odd day
- Leap year: 366 = 52×7 + 2 → 2 odd days

Century odd days:
- 100 years = 76 normal + 24 leap = 76 + 48 = 124 odd days = 5 odd days
- 400 years = (5×4) + 1 = 21 odd days = 0 odd days

Day codes: Sun=0, Mon=1, Tue=2, ..., Sat=6
```

### Clock Problems
```
Angle between hands:
θ = |30H - 5.5M| degrees
(H = hours, M = minutes)

If θ > 180, actual angle = 360 - θ

Hands overlap:
Every 12/11 hours ≈ 65.45 minutes

Hands at right angle:
Twice every hour (except 2-4, 8-10 range)
22 times in 12 hours
```

### Cubes and Dice
```
Painted Cube (n×n×n divided into unit cubes):
- 3 faces painted: 8 (corners)
- 2 faces painted: 12(n-2) (edges)
- 1 face painted: 6(n-2)² (faces)
- 0 faces painted: (n-2)³ (interior)

Standard Dice:
- Opposite faces sum to 7
- 1 opposite to 6
- 2 opposite to 5
- 3 opposite to 4
```

### Venn Diagrams
```
For 3 sets:
n(A∪B∪C) = n(A) + n(B) + n(C) 
           - n(A∩B) - n(B∩C) - n(A∩C) 
           + n(A∩B∩C)

Only A = n(A) - n(A∩B) - n(A∩C) + n(A∩B∩C)

Exactly two sets:
n(A∩B) + n(B∩C) + n(A∩C) - 3×n(A∩B∩C)
```

### Age Problems
```
Key insight: Age difference remains constant

If A is x years older than B:
- A will always be x years older
- Ratio changes with time

"n years ago" means subtract n
"n years hence" means add n

Set up equations using given conditions
```

### Pipes and Cisterns
```
Similar to Work problems:
- Inlet pipe fills in x hours: Rate = 1/x
- Outlet pipe empties in y hours: Rate = -1/y (negative)

Combined rate = Sum of individual rates

Filling with both:
Time = xy/(y-x) hours (if y > x, i.e., filling faster)
```

### Races and Games
```
A beats B by x meters in y meter race:
- When A covers y meters, B covers (y-x) meters
- Ratio of speeds = y : (y-x)

A beats B by t seconds:
- A reaches finish t seconds before B
- Time A takes = (B's time - t)

Head start of x meters:
- A starts from x meters behind starting line
- Effectively races x meters more
```

### 💡 More GATE-Style Practice Problems

**Problem 11 (Clock - GATE Pattern):**
```
At what time between 4 and 5 o'clock are the hands 
of the clock at right angle?

Solution:
Formula: θ = |30H - 5.5M|
For H = 4: θ = |120 - 5.5M|

For 90°:
120 - 5.5M = 90 → M = 30/5.5 ≈ 5.45 minutes
120 - 5.5M = -90 → M = 210/5.5 ≈ 38.18 minutes

First time: 4:05:27 (approximately)
Second time: 4:38:11 (approximately) ✓
```

**Problem 12 (Painted Cube - GATE Pattern):**
```
A 4×4×4 cube is painted on all faces and then cut into 
unit cubes. How many unit cubes have exactly 2 faces painted?

Solution:
For edge pieces (2 faces painted):
Each edge has (n-2) such cubes
A cube has 12 edges

Number = 12 × (4-2) = 12 × 2 = 24 ✓
```

**Problem 13 (Calendar - GATE Pattern):**
```
January 1, 2000 was Saturday. What day is January 1, 2010?

Solution:
Years 2000-2009 (10 years):
Leap years: 2000, 2004, 2008 (3 leap years)
Normal years: 7

Odd days = 7×1 + 3×2 = 7 + 6 = 13 = 6 odd days

Saturday + 6 = Friday

January 1, 2010 is Friday ✓
```

**Problem 14 (Pipes - GATE Pattern):**
```
Pipe A fills a tank in 6 hours, Pipe B in 8 hours.
Pipe C empties it in 12 hours.
If all three work together, how long to fill the tank?

Solution:
A's rate = 1/6 per hour
B's rate = 1/8 per hour
C's rate = -1/12 per hour (negative, empties)

Combined = 1/6 + 1/8 - 1/12
         = 4/24 + 3/24 - 2/24
         = 5/24 per hour

Time = 24/5 = 4.8 hours = 4 hours 48 minutes ✓
```

**Problem 15 (Age Problem - GATE Pattern):**
```
Father is 4 times as old as son. In 20 years, father will be 
twice as old as son. Find their present ages.

Solution:
Let son's age = x, father's age = 4x

In 20 years:
Son = x + 20, Father = 4x + 20

Given: 4x + 20 = 2(x + 20)
4x + 20 = 2x + 40
2x = 20
x = 10

Son = 10 years, Father = 40 years ✓
```
