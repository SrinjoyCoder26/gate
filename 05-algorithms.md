# ⚡ Algorithms - Last Minute Notes

## Quick Navigation
- [Complexity Analysis](#complexity-analysis)
- [Searching Algorithms](#searching-algorithms)
- [Sorting Algorithms](#sorting-algorithms)
- [Divide and Conquer](#divide-and-conquer)
- [Greedy Algorithms](#greedy-algorithms)
- [Dynamic Programming](#dynamic-programming)
- [Graph Algorithms](#graph-algorithms)
- [NP-Completeness](#np-completeness)

---

> **GATE Weightage**: ~10-12% (10-12 marks) | **Expected Questions**: 5-7

---

# Complexity Analysis

## 1. Asymptotic Notations

### 💡 Big-O, Omega, Theta
```
O(g(n)) - Upper Bound (at most)
         f(n) ≤ c·g(n) for n ≥ n₀

Ω(g(n)) - Lower Bound (at least)
         f(n) ≥ c·g(n) for n ≥ n₀

Θ(g(n)) - Tight Bound (exactly)
         c₁·g(n) ≤ f(n) ≤ c₂·g(n) for n ≥ n₀

o(g(n)) - Strict upper bound (less than)
ω(g(n)) - Strict lower bound (greater than)
```

### 💡 Complexity Hierarchy
```
O(1) < O(log n) < O(√n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2^n) < O(n!) < O(n^n)

Polynomial: O(n^k) - Tractable
Exponential: O(k^n) - Intractable
```

### Common Summations
```
1 + 2 + 3 + ... + n = n(n+1)/2 = O(n²)
1 + 2 + 4 + ... + 2^n = 2^(n+1) - 1 = O(2^n)
1 + 1/2 + 1/4 + ... = 2 = O(1)
log 1 + log 2 + ... + log n = log(n!) = Θ(n log n)
```

---

## 2. Recurrence Relations

### 💡 Master Theorem
For T(n) = aT(n/b) + f(n):

| Case | Condition | Result |
|------|-----------|--------|
| 1 | f(n) = O(n^(log_b(a) - ε)) | T(n) = Θ(n^(log_b(a))) |
| 2 | f(n) = Θ(n^(log_b(a))) | T(n) = Θ(n^(log_b(a)) · log n) |
| 3 | f(n) = Ω(n^(log_b(a) + ε)) | T(n) = Θ(f(n)) |

### 💡 Common Recurrences
```
T(n) = T(n/2) + O(1)      → O(log n)      [Binary Search]
T(n) = T(n/2) + O(n)      → O(n)          [Quick Select Avg]
T(n) = 2T(n/2) + O(1)     → O(n)          [Tree Traversal]
T(n) = 2T(n/2) + O(n)     → O(n log n)    [Merge Sort]
T(n) = 2T(n/2) + O(n²)    → O(n²)         [Case 3]
T(n) = T(n-1) + O(1)      → O(n)          [Linear Search]
T(n) = T(n-1) + O(n)      → O(n²)         [Bubble/Selection Sort]
T(n) = 2T(n-1) + O(1)     → O(2^n)        [Tower of Hanoi]
T(n) = T(n-1) + T(n-2)    → O(φ^n) ≈ O(1.618^n) [Fibonacci]
```

---

# Searching Algorithms

## 1. Linear Search
```
Time: O(n)
Space: O(1)
Works on: Unsorted/Sorted arrays
```

## 2. Binary Search

### 💡 Binary Search Algorithm
```c
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;  // Avoid overflow
        if (arr[mid] == key) return mid;
        if (arr[mid] < key) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

### Binary Search Properties
```
Time: O(log n)
Space: O(1) iterative, O(log n) recursive
Requires: Sorted array

Maximum comparisons for n elements = ⌈log₂(n+1)⌉
```

### 💡 Binary Search Variations
```
1. First occurrence: When found, search left half
2. Last occurrence: When found, search right half
3. Count occurrences: (last index - first index + 1)
4. Lower bound: Smallest element ≥ key
5. Upper bound: Smallest element > key
```

---

# Sorting Algorithms

## 💡 Sorting Comparison Table

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Counting Sort | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes |
| Radix Sort | O(d(n+k)) | O(d(n+k)) | O(d(n+k)) | O(n+k) | Yes |
| Bucket Sort | O(n+k) | O(n+k) | O(n²) | O(n) | Yes |

### Memory Trick: Stable Sorts
```
"MIB C R B" - Merge, Insertion, Bubble, Counting, Radix, Bucket
```

---

## 1. Bubble Sort
```c
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        bool swapped = false;
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                swap(arr[j], arr[j+1]);
                swapped = true;
            }
        }
        if (!swapped) break;  // Already sorted
    }
}
```

## 2. Selection Sort
```c
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        int min_idx = i;
        for (int j = i+1; j < n; j++) {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        swap(arr[i], arr[min_idx]);
    }
}
// Always O(n²) comparisons, at most n swaps
```

## 3. Insertion Sort
```c
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i], j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = key;
    }
}
// Best for nearly sorted arrays
```

## 4. Merge Sort

### 💡 Merge Sort Algorithm
```c
void merge(int arr[], int l, int m, int r) {
    // Create temp arrays and merge
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}
```

### Merge Sort Properties
```
Time: O(n log n) always
Space: O(n)
Stable: Yes
Divides in: log n levels
Merging at each level: O(n)
```

## 5. Quick Sort

### 💡 Quick Sort Algorithm
```c
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

### Quick Sort Properties
```
Best/Average: O(n log n) - balanced partitions
Worst: O(n²) - already sorted with bad pivot
Space: O(log n) average, O(n) worst (stack space)
In-place: Yes
Stable: No

Optimization: Randomized pivot or median-of-three
```

## 6. Heap Sort
```
Build Max-Heap: O(n)
Extract max n times: O(n log n)
Total: O(n log n)
In-place: Yes
Stable: No
```

## 7. Counting Sort
```
Time: O(n + k) where k = range of input
Space: O(k)
Works for: Non-negative integers with small range
Stable: Yes
```

## 8. Radix Sort
```
Time: O(d(n + k)) where d = digits, k = base
Best for: Integers with fixed number of digits
Stable: Yes
Uses counting sort as subroutine
```

---

# Divide and Conquer

## 💡 D&C Paradigm
```
1. Divide: Break problem into subproblems
2. Conquer: Solve subproblems recursively
3. Combine: Merge solutions
```

## Important D&C Algorithms

### 1. Binary Search
```
T(n) = T(n/2) + O(1) = O(log n)
```

### 2. Merge Sort
```
T(n) = 2T(n/2) + O(n) = O(n log n)
```

### 3. Quick Sort
```
Best: T(n) = 2T(n/2) + O(n) = O(n log n)
Worst: T(n) = T(n-1) + O(n) = O(n²)
```

### 4. Strassen's Matrix Multiplication
```
Standard: O(n³)
Strassen: O(n^2.81)

T(n) = 7T(n/2) + O(n²)
```

### 5. Karatsuba Multiplication
```
Standard: O(n²)
Karatsuba: O(n^1.585)

For n-digit numbers
```

### 6. Maximum Subarray (Kadane's can also solve in O(n))
```
D&C: T(n) = 2T(n/2) + O(n) = O(n log n)
```

### 7. Closest Pair of Points
```
Brute force: O(n²)
D&C: O(n log n)
```

---

# Greedy Algorithms

## 💡 Greedy Paradigm
```
Make locally optimal choice at each step
Hope it leads to global optimum
Works when problem has:
1. Greedy choice property
2. Optimal substructure
```

## Important Greedy Algorithms

### 1. Activity Selection
```
Sort by finish time
Select first activity, then next compatible
Time: O(n log n)
```

### 2. Fractional Knapsack
```
Calculate value/weight ratio
Sort by ratio descending
Take items greedily
Time: O(n log n)

Note: 0/1 Knapsack requires DP!
```

### 3. Huffman Coding
```
Build optimal prefix-free code
Use min-heap
Time: O(n log n)

Algorithm:
1. Create leaf nodes for each character
2. Repeatedly combine two smallest frequency nodes
3. Assign 0 to left edge, 1 to right edge
```

### 4. Kruskal's MST
```
Sort edges by weight
Add edge if it doesn't form cycle (use Union-Find)
Time: O(E log E)
```

### 5. Prim's MST
```
Start from any vertex
Always add minimum weight edge connecting tree to non-tree vertex
Time: O(E log V) with binary heap
Time: O(E + V log V) with Fibonacci heap
```

### 6. Dijkstra's Shortest Path
```
Single source shortest path
Works only for non-negative weights
Time: O(E log V) with binary heap
```

### 💡 MST Properties
```
For graph with V vertices:
- MST has exactly V-1 edges
- MST is unique if all edge weights distinct
- Cycle property: Max weight edge in cycle not in MST
- Cut property: Min weight edge crossing cut is in MST
```

---

# Dynamic Programming

## 💡 DP Paradigm
```
1. Optimal substructure: Optimal solution contains optimal solutions to subproblems
2. Overlapping subproblems: Same subproblems solved multiple times

Two approaches:
- Top-down: Memoization (recursive + cache)
- Bottom-up: Tabulation (iterative, fill table)
```

## Classic DP Problems

### 1. Fibonacci
```c
// Bottom-up O(n) time, O(1) space
int fib(int n) {
    int a = 0, b = 1;
    for (int i = 2; i <= n; i++) {
        int c = a + b;
        a = b;
        b = c;
    }
    return b;
}
```

### 2. Longest Common Subsequence (LCS)

### 💡 LCS Recurrence
```
LCS(i, j) = 
  LCS(i-1, j-1) + 1           if X[i] == Y[j]
  max(LCS(i-1, j), LCS(i, j-1))  otherwise

Time: O(mn), Space: O(mn) or O(min(m,n))
```

### 3. Longest Increasing Subsequence (LIS)
```
LIS[i] = max(LIS[j]) + 1 for all j < i where arr[j] < arr[i]

Naive: O(n²)
Optimized (Binary Search): O(n log n)
```

### 4. 0/1 Knapsack

### 💡 0/1 Knapsack Recurrence
```
dp[i][w] = max(
    dp[i-1][w],                    // Don't take item i
    dp[i-1][w-weight[i]] + value[i]  // Take item i
)

Time: O(nW), Space: O(nW) or O(W)
Where n = items, W = capacity
```

### 5. Edit Distance (Levenshtein)
```
dp[i][j] = 
  dp[i-1][j-1]                                if X[i] == Y[j]
  1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])  otherwise

Operations: Insert, Delete, Replace
Time: O(mn), Space: O(mn)
```

### 6. Matrix Chain Multiplication
```
dp[i][j] = minimum cost to multiply matrices i to j

dp[i][j] = min(dp[i][k] + dp[k+1][j] + p[i-1]*p[k]*p[j])
           for all k from i to j-1

Time: O(n³), Space: O(n²)
```

### 7. Coin Change
```
Min coins: dp[i] = min(dp[i], dp[i - coin] + 1)
Ways to make: dp[i] += dp[i - coin]

Time: O(n × amount)
```

### 8. Rod Cutting
```
dp[n] = max(price[i] + dp[n-i]) for i = 1 to n
Time: O(n²)
```

### 9. Subset Sum
```
dp[i][sum] = true if sum can be formed using first i elements
dp[i][sum] = dp[i-1][sum] || dp[i-1][sum - arr[i]]
Time: O(n × sum)
```

---

# Graph Algorithms

## 1. BFS & DFS

### 💡 BFS (Breadth-First Search)
```
Uses: Queue
Time: O(V + E)
Applications:
- Shortest path in unweighted graph
- Level order traversal
- Connected components
- Bipartiteness check
```

### 💡 DFS (Depth-First Search)
```
Uses: Stack/Recursion
Time: O(V + E)
Applications:
- Cycle detection
- Topological sort
- Connected components
- Strongly connected components
- Path finding
```

---

## 2. Shortest Path Algorithms

### 💡 Comparison Table
| Algorithm | Graph Type | Time | Space |
|-----------|-----------|------|-------|
| BFS | Unweighted | O(V+E) | O(V) |
| Dijkstra | Non-negative | O(E log V) | O(V) |
| Bellman-Ford | Any | O(VE) | O(V) |
| Floyd-Warshall | All pairs | O(V³) | O(V²) |

### Dijkstra's Algorithm
```
1. Set dist[source] = 0, all others = ∞
2. Use min-heap
3. Extract min, relax all adjacent edges
4. Repeat until heap empty

Cannot handle negative weights!
```

### Bellman-Ford Algorithm
```
1. Set dist[source] = 0, all others = ∞
2. Relax all edges V-1 times
3. If any edge can still be relaxed → negative cycle

Can detect negative cycles!
```

### 💡 Relaxation
```
if dist[u] + weight(u,v) < dist[v]:
    dist[v] = dist[u] + weight(u,v)
    parent[v] = u
```

### Floyd-Warshall Algorithm
```c
for (k = 0; k < V; k++)
    for (i = 0; i < V; i++)
        for (j = 0; j < V; j++)
            dist[i][j] = min(dist[i][j], 
                            dist[i][k] + dist[k][j]);

All-pairs shortest paths
Can detect negative cycles: dist[i][i] < 0
```

---

## 3. Minimum Spanning Tree

### Kruskal's Algorithm
```
1. Sort edges by weight
2. Add edge if it doesn't form cycle
3. Use Union-Find for cycle detection
Time: O(E log E)
```

### Prim's Algorithm
```
1. Start with any vertex
2. Add minimum weight edge to tree
3. Use min-heap for efficiency
Time: O(E log V) with binary heap
```

---

## 4. Topological Sort
```
Only for DAG (Directed Acyclic Graph)
Linear ordering where u comes before v if edge u→v exists

Method 1: DFS-based
- Run DFS, add to front of list on finish
- Time: O(V + E)

Method 2: Kahn's Algorithm (BFS-based)
- Process vertices with in-degree 0
- Time: O(V + E)
```

---

## 5. Strongly Connected Components (SCC)
```
Kosaraju's Algorithm:
1. DFS on original graph, push to stack on finish
2. Transpose graph
3. DFS on transposed graph in stack order

Tarjan's Algorithm:
- Single DFS pass
- Uses low-link values

Time: O(V + E)
```

---

## 6. Articulation Points & Bridges
```
Articulation Point: Vertex whose removal disconnects graph
Bridge: Edge whose removal disconnects graph

Use DFS with discovery time and low values
Time: O(V + E)
```

---

# NP-Completeness

## 💡 Complexity Classes

```
P: Problems solvable in polynomial time
NP: Problems verifiable in polynomial time
NP-Complete: Hardest problems in NP
NP-Hard: At least as hard as NP-Complete

P ⊆ NP
P = NP? (Open problem!)
```

### Relationships
```
P ⊆ NP
NP-Complete ⊆ NP
NP-Complete ⊆ NP-Hard
If any NP-Complete in P, then P = NP
```

## 💡 Famous NP-Complete Problems
```
1. SAT (Boolean Satisfiability) - First NP-Complete
2. 3-SAT
3. Vertex Cover
4. Clique
5. Independent Set
6. Hamiltonian Cycle/Path
7. Traveling Salesman (decision version)
8. Graph Coloring
9. Subset Sum
10. Knapsack (decision version)
11. Partition Problem
```

### Reduction
```
To prove problem X is NP-Complete:
1. Show X ∈ NP (can verify in polynomial time)
2. Reduce known NP-Complete problem to X in polynomial time
```

---

## Quick Memory Tricks 🧠

1. **Stable sorts**: "MIB CRB" - Merge, Insertion, Bubble, Counting, Radix, Bucket
2. **Merge sort space**: O(n) - needs extra array
3. **Quick sort worst case**: Already sorted + bad pivot = O(n²)
4. **Dijkstra fails**: Negative edges
5. **Bellman-Ford**: V-1 relaxations
6. **Floyd-Warshall**: O(V³) for all pairs
7. **MST edges**: Always V-1 for V vertices
8. **DP vs Greedy**: DP for 0/1, Greedy for Fractional

---

## Common Mistakes to Avoid ⚠️

1. Using Dijkstra with negative edges
2. Forgetting Quick Sort is O(n²) worst case
3. Confusing LCS (subsequence) with substring (contiguous)
4. Wrong base cases in DP
5. Not handling disconnected graphs in BFS/DFS
6. Forgetting MST needs V-1 edges
7. Using wrong recurrence for DP problems
8. Confusing NP-Hard and NP-Complete

---

## 📝 GATE Previous Year Patterns

### Most Frequently Asked Topics
1. **Time Complexity Analysis** - 2-3 questions/year
2. **Recurrence Relations** - 1-2 questions/year
3. **Graph Algorithms (MST, Shortest Path)** - 2-3 questions/year
4. **Dynamic Programming** - 2-3 questions/year
5. **Greedy Algorithms** - 1-2 questions/year
6. **Sorting Algorithms** - 1 question/year

### 💡 GATE-Style Practice Problems

**Problem 1 (Complexity - GATE Pattern):**
```c
void fun(int n) {
    int i, j, k;
    for (i = 1; i <= n; i++)
        for (j = 1; j <= i; j++)
            for (k = 1; k <= 100; k++)
                printf("*");
}

Solution:
Total iterations = Σ(i=1 to n) Σ(j=1 to i) 100
= 100 × Σ(i=1 to n) i
= 100 × n(n+1)/2
= 50n² + 50n = O(n²) ✓
```

**Problem 2 (Recurrence - GATE Pattern):**
```
Solve: T(n) = 2T(n/4) + √n

Using Master Theorem:
a = 2, b = 4, f(n) = n^(1/2)
log_b(a) = log_4(2) = 1/2

f(n) = Θ(n^(1/2)) = Θ(n^(log_b(a)))
This is Case 2!

T(n) = Θ(√n × log n) ✓
```

**Problem 3 (Shortest Path - GATE Pattern):**
```
Apply Dijkstra's algorithm from vertex A:

      A --2-- B
      |       |
      4       1
      |       |
      C --3-- D

Order of finalization: A(0) → B(2) → D(3) → C(4)
Wait, let's recalculate:
A = 0
B = 2 (via A)
C = 4 (via A)
D = min(B+1, C+3) = 3 (via B)

Final distances: A=0, B=2, C=4, D=3 ✓
```

**Problem 4 (DP - LCS - GATE Pattern):**
```
Find LCS length of "ABCDGH" and "AEDFHR"

DP Table:
    ""  A  E  D  F  H  R
""   0  0  0  0  0  0  0
A    0  1  1  1  1  1  1
B    0  1  1  1  1  1  1
C    0  1  1  1  1  1  1
D    0  1  1  2  2  2  2
G    0  1  1  2  2  2  2
H    0  1  1  2  2  3  3

LCS length = 3, LCS = "ADH" ✓
```

**Problem 5 (MST - Prim/Kruskal - GATE Pattern):**
```
Find MST weight for graph:
A-B: 4, A-C: 2, B-C: 1, B-D: 5, C-D: 8, C-E: 10, D-E: 2

Kruskal (sort edges):
B-C: 1 ✓
A-C: 2 ✓ 
D-E: 2 ✓
A-B: 4 (skip - cycle)
B-D: 5 ✓

MST edges: B-C, A-C, D-E, B-D
Total weight = 1 + 2 + 2 + 5 = 10 ✓
```

**Problem 6 (Greedy - Activity Selection - GATE Pattern):**
```
Activities: (1,4), (3,5), (0,6), (5,7), (3,8), (5,9), (6,10), (8,11)
Select maximum non-overlapping activities.

Sort by finish time:
(1,4), (3,5), (0,6), (5,7), (3,8), (5,9), (6,10), (8,11)

Greedy selection:
(1,4) ✓
(5,7) ✓ (starts after 4)
(8,11) ✓ (starts after 7)

Maximum activities = 3 ✓
```

**Problem 7 (Topological Sort - GATE Pattern):**
```
Given DAG with edges: A→B, A→C, B→D, C→D, D→E, C→E

Possible topological orders:
A, B, C, D, E ✓
A, C, B, D, E ✓

Number of topological orderings = 2

Using Kahn's algorithm (in-degree):
Initial in-degrees: A=0, B=1, C=1, D=2, E=2
Process A → B and C become 0
Process B → D becomes 1
Process C → D becomes 0, E becomes 1
Process D → E becomes 0
Process E
```

**Problem 8 (Quick Sort Partition - GATE Pattern):**
```
Partition array [10, 7, 8, 9, 1, 5] with last element as pivot.

Pivot = 5
i = -1

j=0: 10 > 5, no swap
j=1: 7 > 5, no swap
j=2: 8 > 5, no swap
j=3: 9 > 5, no swap
j=4: 1 < 5, i=0, swap A[0] and A[4]
     Array: [1, 7, 8, 9, 10, 5]

Final: swap A[i+1] with pivot
Array: [1, 5, 8, 9, 10, 7]

Pivot index = 1 ✓
```

**Problem 9 (0/1 Knapsack - GATE Pattern):**
```
Items: weights = [2, 3, 4, 5], values = [3, 4, 5, 6]
Capacity W = 5

DP Table:
    0  1  2  3  4  5
0   0  0  0  0  0  0
1   0  0  3  3  3  3
2   0  0  3  4  4  7
3   0  0  3  4  5  7
4   0  0  3  4  5  7

Maximum value = 7 (items with weights 2 and 3) ✓
```

**Problem 10 (Bellman-Ford - GATE Pattern):**
```
Detect if graph has negative cycle:
A→B: 1, B→C: -1, C→A: -1

After |V|-1 = 2 iterations from A:
d[A]=0, d[B]=1, d[C]=0

Third iteration check:
Edge A→B: d[B] > d[A] + 1? No
Edge B→C: d[C] > d[B] + (-1) = 0? No
Edge C→A: d[A] > d[C] + (-1) = -1? Yes!

Negative cycle detected! ✓
```

---

## 📊 Formula Quick Reference Sheet

### Master Theorem
```
T(n) = aT(n/b) + f(n)

Compare f(n) with n^(log_b(a)):
Case 1: f(n) = O(n^(log_b(a) - ε)) → T(n) = Θ(n^(log_b(a)))
Case 2: f(n) = Θ(n^(log_b(a))) → T(n) = Θ(n^(log_b(a)) log n)
Case 3: f(n) = Ω(n^(log_b(a) + ε)) → T(n) = Θ(f(n))
```

### Sorting Complexities
```
Comparison-based lower bound: Ω(n log n)
Non-comparison (Counting, Radix, Bucket): O(n)

Stable sorts: Merge, Insertion, Bubble, Counting, Radix
In-place: Quick, Heap, Selection, Insertion, Bubble
```

### Graph Algorithms
```
BFS/DFS: O(V + E)
Dijkstra (binary heap): O((V + E) log V)
Bellman-Ford: O(VE)
Floyd-Warshall: O(V³)
Prim (binary heap): O((V + E) log V)
Kruskal (Union-Find): O(E log E)
Topological Sort: O(V + E)
```

### DP Problems
```
LCS: O(mn) time, O(mn) space
LIS: O(n²) naive, O(n log n) optimal
0/1 Knapsack: O(nW)
Edit Distance: O(mn)
Matrix Chain: O(n³)
Coin Change: O(n × amount)
```

### NP-Completeness
```
P ⊆ NP
NP-Complete = NP ∩ NP-Hard
If any NP-Complete ∈ P, then P = NP

Famous NP-Complete:
SAT, 3-SAT, Vertex Cover, Clique, Independent Set,
Hamiltonian Cycle, TSP (decision), Subset Sum, Graph Coloring
```
