# 💻 Programming & Data Structures - Last Minute Notes

## Quick Navigation
- [C Programming Fundamentals](#c-programming-fundamentals)
- [Pointers](#pointers)
- [Arrays and Strings](#arrays-and-strings)
- [Structures and Unions](#structures-and-unions)
- [Recursion](#recursion)
- [Data Structures](#data-structures)

---

# C Programming Fundamentals

## 1. Data Types & Storage

### 💡 Data Type Sizes (Typical 32/64-bit system)
| Data Type | Size (bytes) | Range |
|-----------|--------------|-------|
| char | 1 | -128 to 127 or 0 to 255 |
| short | 2 | -32,768 to 32,767 |
| int | 4 | -2^31 to 2^31 - 1 |
| long | 4/8 | System dependent |
| float | 4 | 7 decimal digits |
| double | 8 | 15 decimal digits |
| pointer | 4/8 | System dependent |

### Storage Classes
| Class | Scope | Lifetime | Default Value |
|-------|-------|----------|---------------|
| **auto** | Local | Function | Garbage |
| **register** | Local | Function | Garbage |
| **static** | Local/Global | Program | 0 |
| **extern** | Global | Program | 0 |

```c
static int x = 5;    // Retains value between function calls
extern int y;        // Declared elsewhere
register int z = 10; // Hint to store in CPU register
```

---

## 2. Operators

### 💡 Operator Precedence (High to Low)
```
() [] -> .                    Highest
! ~ ++ -- + - * & (type) sizeof
* / %
+ -
<< >>
< <= > >=
== !=
&
^
|
&&
||
?:
= += -= *= /= etc.
,                             Lowest
```

### 💡 Important Operator Details
```c
// Pre-increment vs Post-increment
int a = 5;
int b = ++a;  // a = 6, b = 6 (increment then assign)
int c = a++;  // a = 7, c = 6 (assign then increment)

// Bitwise operators
& (AND), | (OR), ^ (XOR), ~ (NOT)
<< (Left shift: multiply by 2^n)
>> (Right shift: divide by 2^n)

// Conditional operator
result = (condition) ? value_if_true : value_if_false;

// Comma operator - returns last value
x = (a, b, c);  // x = c
```

### sizeof Operator
```c
sizeof(int)     // Usually 4
sizeof(char)    // Always 1
sizeof(array)   // Total bytes in array
sizeof(pointer) // 4 or 8 (system dependent)

// For array passed to function, sizeof gives pointer size, not array size!
```

---

## 3. Control Flow

### Switch Statement Rules
```c
switch(expression) {  // expression must be integral type
    case constant1:   // constants only (no variables)
        // statements
        break;        // without break, falls through
    case constant2:
        // statements
        break;
    default:
        // statements
}
```

### Loop Equivalence
```c
// for loop
for(init; condition; update) { body; }

// Equivalent while loop
init;
while(condition) { body; update; }
```

---

# Pointers

## 1. Pointer Basics

### 💡 Pointer Operations
```c
int x = 10;
int *p = &x;      // p stores address of x

*p = 20;          // Dereference: changes x to 20
p++;              // Pointer arithmetic: moves by sizeof(int)

printf("%d", x);   // 20
printf("%p", p);   // Address
printf("%d", *p);  // Value at address (but p was incremented!)
```

### Pointer Arithmetic
```c
int arr[5] = {10, 20, 30, 40, 50};
int *p = arr;

p + 1      // Address of arr[1]
*(p + 1)   // Value 20
p[1]       // Same as *(p + 1) = 20

p - arr    // Number of elements between (0 if p = arr)
p2 - p1    // Difference in number of elements
```

---

## 2. Pointer Types

### 💡 Pointer Declarations
```c
int *p;          // Pointer to int
int **pp;        // Pointer to pointer to int
int *arr[10];    // Array of 10 pointers to int
int (*ptr)[10];  // Pointer to array of 10 ints
int (*fp)(int);  // Pointer to function taking int, returning int
```

### Reading Complex Declarations (Right-Left Rule)
```c
int *(*p)[10];
// p is pointer to array of 10 pointers to int

int (*f[5])(int);
// f is array of 5 pointers to functions taking int, returning int
```

---

## 3. Pointers and Arrays

### 💡 Key Relationships
```c
int arr[5] = {1, 2, 3, 4, 5};

arr        // Same as &arr[0]
arr + i    // Same as &arr[i]
*(arr + i) // Same as arr[i]
&arr       // Pointer to entire array (different type!)

// Key difference:
int *p = arr;
sizeof(arr)  // 20 (5 * sizeof(int))
sizeof(p)    // 4 or 8 (pointer size)
```

### 2D Array vs Pointer to Pointer
```c
int arr[3][4];       // Contiguous memory, 12 ints
int **p;             // Pointer to pointer

arr[i][j]     = *(*(arr + i) + j)
// arr + i gives row address
// *(arr + i) gives first element of row i
// *(arr + i) + j gives address of element [i][j]
```

---

## 4. Pointers and Functions

### 💡 Pass by Reference
```c
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int x = 5, y = 10;
swap(&x, &y);  // x = 10, y = 5
```

### Returning Pointers
```c
// WRONG - returns pointer to local variable
int* foo() {
    int x = 10;
    return &x;  // x is destroyed after function returns!
}

// CORRECT - return pointer to static or malloc'd memory
int* bar() {
    static int x = 10;  // OK
    return &x;
}

int* baz() {
    int *p = (int*)malloc(sizeof(int));  // OK
    *p = 10;
    return p;
}
```

---

# Arrays and Strings

## 1. Array Basics

### 💡 Array Initialization
```c
int arr[5];              // Uninitialized (garbage values)
int arr[5] = {0};        // All zeros
int arr[] = {1,2,3};     // Size = 3
int arr[5] = {1,2};      // {1, 2, 0, 0, 0}

// 2D array
int arr[2][3] = {{1,2,3}, {4,5,6}};
int arr[][3] = {{1,2,3}, {4,5,6}};  // First dimension optional
```

### Array Memory Layout
```c
// 2D array arr[3][4] stored row-major:
// arr[0][0], arr[0][1], arr[0][2], arr[0][3],
// arr[1][0], arr[1][1], arr[1][2], arr[1][3],
// arr[2][0], arr[2][1], arr[2][2], arr[2][3]

// Address of arr[i][j] in arr[m][n]:
// Base + (i * n + j) * sizeof(element)
```

---

## 2. Strings

### 💡 String Basics
```c
char str1[] = "Hello";        // Size = 6 (includes '\0')
char str2[10] = "Hello";      // "Hello\0\0\0\0\0"
char *str3 = "Hello";         // Pointer to string literal (read-only!)

strlen(str1);   // 5 (doesn't count '\0')
sizeof(str1);   // 6 (counts '\0')
```

### 💡 String Functions
```c
#include <string.h>

strlen(s)           // Length (excluding '\0')
strcpy(dest, src)   // Copy src to dest
strncpy(d, s, n)    // Copy at most n chars
strcat(dest, src)   // Concatenate
strncat(d, s, n)    // Concatenate at most n chars
strcmp(s1, s2)      // Compare: <0, 0, >0
strncmp(s1, s2, n)  // Compare first n chars
strchr(s, c)        // First occurrence of c
strrchr(s, c)       // Last occurrence of c
strstr(s1, s2)      // Find substring s2 in s1
```

---

# Structures and Unions

## 1. Structures

### 💡 Structure Basics
```c
struct Point {
    int x;
    int y;
};

struct Point p1 = {10, 20};
struct Point p2;
p2.x = 5;
p2.y = 15;

struct Point *ptr = &p1;
ptr->x = 30;  // Same as (*ptr).x = 30
```

### Structure Padding/Alignment
```c
struct Example {
    char a;     // 1 byte + 3 padding
    int b;      // 4 bytes
    char c;     // 1 byte + 3 padding
};
// Total: 12 bytes (not 6!)

// Rule: Each member aligned to its own size
// Struct size = multiple of largest member
```

### 💡 Avoid Padding
```c
// Method 1: Order by decreasing size
struct Better {
    int b;      // 4 bytes
    char a;     // 1 byte
    char c;     // 1 byte + 2 padding
};
// Total: 8 bytes

// Method 2: #pragma pack(1) - compiler specific
#pragma pack(1)
struct Packed {
    char a;
    int b;
    char c;
};
// Total: 6 bytes (no padding)
```

---

## 2. Unions

### 💡 Union Basics
```c
union Data {
    int i;
    float f;
    char str[20];
};

// Size = size of largest member (20 bytes here)
// All members share same memory!

union Data d;
d.i = 10;       // Now i is valid
d.f = 3.14;     // Now f is valid, i is garbage
```

### Structure vs Union
| Feature | Structure | Union |
|---------|-----------|-------|
| Memory | Sum of all members | Size of largest member |
| Access | All members valid | Only last written member valid |
| Use | Group related data | Memory sharing |

---

## 3. Self-Referential Structures

```c
struct Node {
    int data;
    struct Node *next;  // Pointer to same type
};

// Used in: Linked lists, Trees, Graphs
```

---

# Recursion

## 1. Recursion Basics

### 💡 Recursion Formula
```c
// General pattern
returnType function(parameters) {
    if (base_case) {
        return base_value;
    }
    return recursive_expression;
}
```

### Stack Memory in Recursion
```
Each recursive call:
1. Creates new stack frame
2. Stores parameters, local variables, return address
3. Stack grows with each call
4. Stack unwinding on return

Stack overflow if: Too many recursive calls
```

---

## 2. Common Recursive Functions

### 💡 Factorial
```c
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
// T(n) = T(n-1) + O(1) = O(n)
```

### Fibonacci
```c
// Naive - O(2^n)
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}

// Memoized - O(n)
int fib_memo(int n, int memo[]) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    memo[n] = fib_memo(n-1, memo) + fib_memo(n-2, memo);
    return memo[n];
}
```

### Binary Search
```c
int binarySearch(int arr[], int low, int high, int key) {
    if (low > high) return -1;
    int mid = low + (high - low) / 2;
    if (arr[mid] == key) return mid;
    if (arr[mid] > key)
        return binarySearch(arr, low, mid - 1, key);
    return binarySearch(arr, mid + 1, high, key);
}
// T(n) = T(n/2) + O(1) = O(log n)
```

---

## 3. Tail Recursion

### 💡 Tail Recursion
```c
// Tail recursive - last operation is recursive call
int factorialTail(int n, int acc) {
    if (n <= 1) return acc;
    return factorialTail(n - 1, n * acc);
}
// Call: factorialTail(5, 1)

// Non-tail recursive - operation after recursive call
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);  // Multiplication after call
}
```

**Advantage**: Tail recursion can be optimized by compiler to iteration (no stack growth)

---

# Data Structures

## 1. Linked Lists

### 💡 Types of Linked Lists
| Type | Features |
|------|----------|
| **Singly** | Each node has data + next pointer |
| **Doubly** | Each node has data + prev + next pointers |
| **Circular** | Last node points to first |

### Singly Linked List Operations
```c
struct Node {
    int data;
    struct Node *next;
};

// Insert at beginning: O(1)
void insertFront(struct Node **head, int data) {
    struct Node *new = (struct Node*)malloc(sizeof(struct Node));
    new->data = data;
    new->next = *head;
    *head = new;
}

// Insert at end: O(n)
// Delete: O(n) to find, O(1) to remove
// Search: O(n)
```

### 💡 Array vs Linked List
| Operation | Array | Linked List |
|-----------|-------|-------------|
| Access | O(1) | O(n) |
| Insert at beginning | O(n) | O(1) |
| Insert at end | O(1)* | O(n) or O(1)** |
| Insert at middle | O(n) | O(1)*** |
| Delete | O(n) | O(1)*** |
| Search | O(n), O(log n)**** | O(n) |
| Memory | Contiguous | Scattered |

*Amortized; **With tail pointer; ***After finding position; ****If sorted

---

## 2. Stacks

### 💡 Stack Operations (LIFO)
```c
// Array implementation
#define MAX 100
int stack[MAX], top = -1;

void push(int x) {
    if (top == MAX - 1) return;  // Overflow
    stack[++top] = x;
}

int pop() {
    if (top == -1) return -1;    // Underflow
    return stack[top--];
}

int peek() {
    if (top == -1) return -1;
    return stack[top];
}

int isEmpty() { return top == -1; }
```

### Time Complexities
```
Push: O(1)
Pop: O(1)
Peek/Top: O(1)
Search: O(n)
```

### 💡 Stack Applications
1. **Expression conversion**: Infix → Postfix → Prefix
2. **Expression evaluation**: Postfix, Prefix
3. **Function calls**: Call stack
4. **Parenthesis matching**
5. **Undo operations**
6. **Browser history (back button)**
7. **DFS implementation**

### Infix to Postfix Conversion
```
Algorithm:
1. If operand, add to output
2. If '(', push to stack
3. If ')', pop until '('
4. If operator:
   - Pop higher/equal precedence operators to output
   - Push current operator

Example: A + B * C → A B C * +
         (A + B) * C → A B + C *
```

---

## 3. Queues

### 💡 Queue Operations (FIFO)
```c
// Circular array implementation
#define MAX 100
int queue[MAX], front = 0, rear = -1, size = 0;

void enqueue(int x) {
    if (size == MAX) return;  // Full
    rear = (rear + 1) % MAX;
    queue[rear] = x;
    size++;
}

int dequeue() {
    if (size == 0) return -1;  // Empty
    int item = queue[front];
    front = (front + 1) % MAX;
    size--;
    return item;
}
```

### Types of Queues
| Type | Description |
|------|-------------|
| **Simple Queue** | FIFO |
| **Circular Queue** | Rear wraps to front |
| **Deque** | Insert/delete at both ends |
| **Priority Queue** | Elements have priority |

### 💡 Queue Applications
1. **BFS implementation**
2. **CPU scheduling**
3. **Print queue**
4. **Buffer for devices**
5. **Level-order traversal**

---

## 4. Trees

### 💡 Binary Tree Basics
```c
struct TreeNode {
    int data;
    struct TreeNode *left, *right;
};
```

### Binary Tree Properties
```
Maximum nodes at level L = 2^L  (root at level 0)
Maximum nodes in tree of height H = 2^(H+1) - 1
Minimum height for N nodes = ⌈log₂(N+1)⌉ - 1
For N nodes: Edges = N - 1
If N0 = leaf nodes, N2 = nodes with 2 children: N0 = N2 + 1
```

### 💡 Tree Traversals
```c
// Inorder (Left, Root, Right) - gives sorted order for BST
void inorder(Node *root) {
    if (root == NULL) return;
    inorder(root->left);
    printf("%d ", root->data);
    inorder(root->right);
}

// Preorder (Root, Left, Right)
void preorder(Node *root) {
    if (root == NULL) return;
    printf("%d ", root->data);
    preorder(root->left);
    preorder(root->right);
}

// Postorder (Left, Right, Root)
void postorder(Node *root) {
    if (root == NULL) return;
    postorder(root->left);
    postorder(root->right);
    printf("%d ", root->data);
}

// Level Order (BFS) - uses queue
```

### 💡 Memory Trick for Traversals
```
In-order:  LNR (Left, Node, Right)
Pre-order: NLR (Node, Left, Right)
Post-order: LRN (Left, Right, Node)

"N" moves from middle to front to back
```

---

## 5. Binary Search Tree (BST)

### 💡 BST Properties
```
For every node:
- All nodes in left subtree < node
- All nodes in right subtree > node
- Both subtrees are also BSTs
```

### BST Operations
| Operation | Average | Worst (skewed) |
|-----------|---------|----------------|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Inorder | O(n) | O(n) |

### BST Deletion Cases
```
1. Node is leaf: Simply remove
2. Node has one child: Replace with child
3. Node has two children: 
   - Replace with inorder successor (smallest in right subtree)
   - Or replace with inorder predecessor (largest in left subtree)
```

---

## 6. Heaps

### 💡 Heap Properties
```
Max-Heap: Parent ≥ Children
Min-Heap: Parent ≤ Children

Complete binary tree stored in array:
- Parent of node i: ⌊(i-1)/2⌋
- Left child of i: 2i + 1
- Right child of i: 2i + 2

For 1-based indexing:
- Parent: i/2, Left: 2i, Right: 2i + 1
```

### Heap Operations
| Operation | Time Complexity |
|-----------|-----------------|
| Insert | O(log n) |
| Delete max/min | O(log n) |
| Get max/min | O(1) |
| Build heap | O(n) |
| Heapify | O(log n) |

### 💡 Heap Applications
1. **Heap Sort**: O(n log n)
2. **Priority Queue**
3. **Kth largest/smallest element**
4. **Merge K sorted arrays**

---

## 7. Hashing

### 💡 Hash Functions
```c
// Division Method
h(k) = k mod m  // m = table size (prefer prime)

// Multiplication Method
h(k) = ⌊m(kA mod 1)⌋  // A ≈ 0.6180339... (golden ratio)
```

### Collision Resolution

#### 1. Chaining (Separate Chaining)
```
Each bucket is a linked list
Load factor α = n/m (can be > 1)

Average case:
- Successful search: 1 + α/2
- Unsuccessful search: 1 + α
```

#### 2. Open Addressing
```
All elements stored in table itself

a) Linear Probing:
   h(k, i) = (h'(k) + i) mod m
   Problem: Primary clustering

b) Quadratic Probing:
   h(k, i) = (h'(k) + c₁i + c₂i²) mod m
   Problem: Secondary clustering

c) Double Hashing:
   h(k, i) = (h₁(k) + i·h₂(k)) mod m
   Best distribution

Load factor α < 1 required
```

### 💡 Hash Table Complexities
| Operation | Average | Worst |
|-----------|---------|-------|
| Search | O(1) | O(n) |
| Insert | O(1) | O(n) |
| Delete | O(1) | O(n) |

---

## 8. Graphs

### 💡 Graph Representations

**Adjacency Matrix**
```
Space: O(V²)
Check edge: O(1)
List neighbors: O(V)
Add edge: O(1)
Good for: Dense graphs
```

**Adjacency List**
```
Space: O(V + E)
Check edge: O(degree)
List neighbors: O(degree)
Add edge: O(1)
Good for: Sparse graphs
```

### Graph Traversals
```
BFS (Breadth-First Search):
- Uses Queue
- Level by level
- Time: O(V + E)
- Finds shortest path in unweighted graph

DFS (Depth-First Search):
- Uses Stack/Recursion
- Go deep first
- Time: O(V + E)
- Applications: Cycle detection, topological sort
```

---

## Quick Memory Tricks 🧠

1. **Pointer**: "Address holder" - `*` dereferences, `&` gets address
2. **String length**: strlen doesn't count '\0', sizeof does
3. **Stack**: LIFO - "Last plate you put is first you take"
4. **Queue**: FIFO - "First in line gets served first"
5. **BST Inorder**: Gives sorted sequence
6. **Heap parent/child**: For 0-indexed: parent = (i-1)/2, left = 2i+1, right = 2i+2
7. **Hash load factor**: α = n/m; keep α < 1 for open addressing

---

## Common Mistakes to Avoid ⚠️

1. Dereferencing NULL pointer
2. Memory leaks (malloc without free)
3. Array out of bounds access
4. Modifying string literals (`char *s = "hello"; s[0] = 'H';` - crash!)
5. Using == instead of strcmp for strings
6. Forgetting to handle empty cases (empty list, tree, stack)
7. Off-by-one errors in loops
8. Stack overflow in deep recursion
9. Forgetting that array passed to function decays to pointer
10. Structure padding affecting sizeof
