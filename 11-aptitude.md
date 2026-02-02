# 🧮 General Aptitude - Last Minute Notes

## Quick Navigation
- [Quantitative Aptitude](#quantitative-aptitude)
- [Verbal Ability](#verbal-ability)
- [Logical Reasoning](#logical-reasoning)

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
