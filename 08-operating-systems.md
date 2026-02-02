# 🖥️ Operating Systems - Last Minute Notes

## Quick Navigation
- [Process Management](#process-management)
- [Process Synchronization](#process-synchronization)
- [Deadlocks](#deadlocks)
- [Memory Management](#memory-management)
- [Virtual Memory](#virtual-memory)
- [File Systems](#file-systems)
- [Disk Scheduling](#disk-scheduling)

---

# Process Management

## 1. Process Concepts

### 💡 Process States
```
        ┌─────────────┐
        │    New      │
        └──────┬──────┘
               ↓
        ┌──────┴──────┐
        │    Ready    │←─────────────┐
        └──────┬──────┘              │
               ↓ (Dispatch)          │ (I/O Complete)
        ┌──────┴──────┐              │
        │   Running   │──────────────┤
        └──────┬──────┘              │
               │ (I/O Request)       │
               ↓                     │
        ┌──────┴──────┐              │
        │   Waiting   │──────────────┘
        └─────────────┘
               │
               ↓
        ┌─────────────┐
        │ Terminated  │
        └─────────────┘
```

### Process Control Block (PCB)
```
Contains:
• Process ID (PID)
• Process state
• Program counter
• CPU registers
• Memory management info
• I/O status info
• Scheduling info
• Accounting info
```

---

## 2. Process vs Thread

### 💡 Comparison
| Aspect | Process | Thread |
|--------|---------|--------|
| Memory | Separate address space | Shared address space |
| Creation | Heavy (fork) | Light |
| Communication | IPC needed | Direct memory sharing |
| Context switch | Slow | Fast |
| Independence | Independent | Share resources |

### Types of Threads
```
User-level threads:
• Managed by user library
• Kernel unaware
• Fast context switch
• One blocks all

Kernel-level threads:
• Managed by kernel
• Kernel aware
• Slower context switch
• One block doesn't affect others
```

---

## 3. CPU Scheduling

### 💡 Scheduling Criteria
```
• CPU Utilization: Keep CPU busy
• Throughput: Processes completed per unit time
• Turnaround Time: Total time from submission to completion
• Waiting Time: Time spent in ready queue
• Response Time: Time from submission to first response
```

### 💡 Scheduling Algorithms

| Algorithm | Preemptive | Starvation | Convoy Effect |
|-----------|------------|------------|---------------|
| FCFS | No | No | Yes |
| SJF | No | Yes | No |
| SRTF | Yes | Yes | No |
| Priority | Both | Yes | No |
| Round Robin | Yes | No | No |

### Formulas
```
Turnaround Time (TAT) = Completion Time - Arrival Time
Waiting Time (WT) = Turnaround Time - Burst Time
Response Time (RT) = First Response - Arrival Time

Throughput = Number of processes / Total time
```

---

### FCFS (First Come First Serve)
```
• Non-preemptive
• Simple FIFO queue
• Convoy effect: Short processes wait for long ones
• Average waiting time can be high
```

### SJF (Shortest Job First)
```
• Non-preemptive
• Optimal for average waiting time
• Starvation possible for long processes
• Requires knowing burst time in advance
```

### SRTF (Shortest Remaining Time First)
```
• Preemptive version of SJF
• New shorter process preempts current
• Optimal for average waiting time
• Starvation possible
```

### Priority Scheduling
```
• Higher priority runs first
• Can be preemptive or non-preemptive
• Starvation: Low priority may never run
• Solution: Aging (increase priority over time)
```

### 💡 Round Robin (RR)
```
• Preemptive, uses time quantum q
• Each process gets q time units
• After q, moved to end of queue

Time quantum choice:
• Too small: High context switch overhead
• Too large: Becomes FCFS
• Typical: 10-100 ms

Average waiting time depends on q and process mix
```

---

### Multilevel Queue Scheduling
```
Multiple queues with different priorities
Each queue has its own algorithm
Process permanently assigned to queue
```

### Multilevel Feedback Queue
```
Processes can move between queues
New process starts in highest priority queue
If uses full quantum, demoted to lower queue
I/O-bound processes stay in higher queues
```

---

# Process Synchronization

## 1. Critical Section Problem

### 💡 Requirements
```
1. Mutual Exclusion: Only one process in CS at a time
2. Progress: If no one in CS, selection can't be postponed
3. Bounded Waiting: Limit on waiting time
```

### Peterson's Solution (2 processes)
```c
// Process i
flag[i] = true;
turn = j;
while (flag[j] && turn == j);  // Busy wait
// Critical Section
flag[i] = false;
```

---

## 2. Semaphores

### 💡 Types
```
Counting Semaphore: Any integer value
Binary Semaphore (Mutex): Only 0 or 1
```

### Semaphore Operations
```c
wait(S) / P(S) / down(S):
    while (S <= 0);  // Busy wait
    S--;

signal(S) / V(S) / up(S):
    S++;
```

### 💡 Semaphore Usage
```c
// Mutual Exclusion (mutex = 1)
wait(mutex);
// Critical Section
signal(mutex);

// Synchronization (sync = 0)
// P1: signal(sync);  after statement A
// P2: wait(sync);    before statement B
// B executes only after A
```

---

## 3. Classic Synchronization Problems

### 💡 Producer-Consumer (Bounded Buffer)
```c
Semaphores: mutex = 1, empty = n, full = 0

Producer:
    wait(empty);
    wait(mutex);
    // Add item
    signal(mutex);
    signal(full);

Consumer:
    wait(full);
    wait(mutex);
    // Remove item
    signal(mutex);
    signal(empty);
```

### 💡 Reader-Writer Problem
```c
Semaphores: mutex = 1, wrt = 1
int readcount = 0;

Reader:
    wait(mutex);
    readcount++;
    if (readcount == 1) wait(wrt);
    signal(mutex);
    // Read
    wait(mutex);
    readcount--;
    if (readcount == 0) signal(wrt);
    signal(mutex);

Writer:
    wait(wrt);
    // Write
    signal(wrt);
```

### 💡 Dining Philosophers
```
5 philosophers, 5 forks
Each needs 2 forks to eat
Naive solution causes deadlock

Solutions:
1. Allow at most 4 philosophers at table
2. Pick up both forks only if both available
3. Odd philosophers pick left first, even pick right first
```

---

## 4. Monitors

```
High-level synchronization construct
Mutual exclusion automatic
Uses condition variables:
• wait(): Suspend calling process
• signal(): Resume one waiting process
```

---

# Deadlocks

## 1. Deadlock Conditions

### 💡 Four Necessary Conditions
```
1. Mutual Exclusion: Resource can't be shared
2. Hold and Wait: Process holds while waiting for more
3. No Preemption: Resources can't be forcibly taken
4. Circular Wait: Cycle in resource allocation graph
```

---

## 2. Resource Allocation Graph

### 💡 Graph Analysis
```
• Request edge: Process → Resource
• Assignment edge: Resource → Process

No cycle → No deadlock
Cycle exists:
  - Single instance per resource → Deadlock
  - Multiple instances → May or may not be deadlock
```

---

## 3. Deadlock Handling

### 💡 Strategies
```
1. Prevention: Ensure at least one condition never holds
2. Avoidance: Don't grant requests that may lead to deadlock
3. Detection & Recovery: Let deadlock occur, then handle
4. Ignorance: Ostrich algorithm (do nothing)
```

### Deadlock Prevention
```
Mutual Exclusion: Can't prevent for non-sharable resources
Hold and Wait: Request all resources at once
No Preemption: Allow preemption if blocked
Circular Wait: Impose ordering on resource requests
```

---

## 4. Banker's Algorithm

### 💡 Data Structures
```
n = processes, m = resources

Available[m]: Available instances of each resource
Max[n][m]: Maximum demand of each process
Allocation[n][m]: Currently allocated to each process
Need[n][m]: Remaining need (Max - Allocation)
```

### 💡 Safety Algorithm
```
1. Work = Available, Finish[i] = false for all i
2. Find i where Finish[i] = false AND Need[i] ≤ Work
3. Work = Work + Allocation[i], Finish[i] = true
4. Repeat step 2
5. If all Finish[i] = true → Safe state
```

### 💡 Resource Request Algorithm
```
Request_i = request vector for process i

1. If Request_i > Need_i → Error
2. If Request_i > Available → Wait
3. Pretend to allocate:
   Available -= Request_i
   Allocation_i += Request_i
   Need_i -= Request_i
4. Run safety algorithm
5. If safe → Grant, else → Wait (rollback)
```

---

# Memory Management

## 1. Memory Allocation

### 💡 Contiguous Allocation
```
Fixed Partitioning:
• Memory divided into fixed-size partitions
• Internal fragmentation

Variable Partitioning:
• Partitions created as needed
• External fragmentation
```

### 💡 Allocation Strategies
| Strategy | Description | Performance |
|----------|-------------|-------------|
| First Fit | First hole that fits | Fast, good |
| Best Fit | Smallest hole that fits | Leaves small fragments |
| Worst Fit | Largest hole | Poor |
| Next Fit | From last allocation point | Moderate |

### Fragmentation
```
Internal: Allocated memory > Required memory
External: Total free memory sufficient but not contiguous

Solution for external: Compaction, Paging
```

---

## 2. Paging

### 💡 Paging Concepts
```
Physical memory → Frames (fixed size)
Logical memory → Pages (same size as frames)
Page Table: Maps page number to frame number

Page Size = Frame Size = 2^k bytes (typically 4KB)
```

### 💡 Address Translation
```
Logical Address: [Page Number | Page Offset]
Physical Address: [Frame Number | Page Offset]

Page number bits = ⌈log₂(number of pages)⌉
Page offset bits = ⌈log₂(page size)⌉

Frame number obtained from page table
Page offset copied directly
```

### Example
```
Logical address space = 32 bits
Page size = 4 KB = 2^12 bytes

Page offset = 12 bits
Page number = 32 - 12 = 20 bits
Number of pages = 2^20 = 1M pages
```

### 💡 Translation Lookaside Buffer (TLB)
```
Cache for page table entries
TLB hit: 1 memory access
TLB miss: 2 memory accesses (page table + data)

Effective Access Time (EAT):
EAT = h × (TLB_time + Mem_time) + (1-h) × (TLB_time + 2×Mem_time)

Where h = hit ratio
```

### Multilevel Page Tables
```
Break page table into multiple levels
Only active portions in memory
Reduces memory overhead

Two-level example:
Logical Address: [p1 | p2 | offset]
```

---

## 3. Segmentation

### 💡 Segmentation Concepts
```
Memory divided by logical units (code, data, stack)
Variable-size segments
Segment Table: (base, limit) for each segment

Logical Address: [Segment Number | Offset]
Physical Address: base + offset (if offset < limit)
```

### Paging vs Segmentation
| Feature | Paging | Segmentation |
|---------|--------|--------------|
| Size | Fixed | Variable |
| Fragmentation | Internal | External |
| View | Physical | Logical |
| Sharing | Harder | Easier |

---

# Virtual Memory

## 1. Demand Paging

### 💡 Concepts
```
Pages loaded only when needed (lazy loading)
Valid/Invalid bit in page table
Page fault: Required page not in memory

Page Fault Handling:
1. Trap to OS
2. Find page on disk
3. Find free frame (or evict)
4. Load page into frame
5. Update page table
6. Restart instruction
```

### 💡 Effective Access Time with Page Faults
```
EAT = (1 - p) × memory_access_time + p × page_fault_time

Where p = page fault rate
Page fault time includes: disk I/O, page table update, restart
```

---

## 2. Page Replacement Algorithms

### 💡 Algorithm Comparison
| Algorithm | Description | Belady's Anomaly |
|-----------|-------------|------------------|
| FIFO | Replace oldest page | Yes |
| Optimal | Replace page used farthest in future | No |
| LRU | Replace least recently used | No |
| LRU-Approximation | Second chance, etc. | Varies |

### 💡 FIFO (First In First Out)
```
Replace oldest page in memory
Simple but not optimal
Suffers from Belady's Anomaly:
More frames can cause MORE page faults
```

### 💡 Optimal (OPT)
```
Replace page used farthest in future
Lowest page faults (theoretical best)
Not implementable (needs future knowledge)
Used as benchmark
```

### 💡 LRU (Least Recently Used)
```
Replace page not used for longest time
Good performance
Implementation options:
• Counter: Record time of last use
• Stack: Move accessed page to top
```

### 💡 Second Chance (Clock Algorithm)
```
FIFO with reference bit
If reference bit = 1, give second chance (set to 0)
If reference bit = 0, replace
Approximates LRU with less overhead
```

### 💡 Page Fault Calculation Example
```
Reference string: 7, 0, 1, 2, 0, 3, 0, 4, 2, 3
3 frames

FIFO:
[7] [7,0] [7,0,1] [2,0,1] [2,0,1] [2,3,1] [2,3,0] [4,3,0] [4,2,0] [4,2,3]
Page faults: 9

Optimal:
[7] [7,0] [7,0,1] [2,0,1] [2,0,1] [2,0,3] [2,0,3] [2,4,3] [2,4,3] [2,4,3]
Page faults: 6

LRU:
[7] [7,0] [7,0,1] [2,0,1] [2,0,1] [2,0,3] [2,0,3] [4,0,3] [4,0,2] [4,3,2]
Page faults: 7
```

---

## 3. Thrashing

### 💡 Thrashing
```
Process spends more time paging than executing
Cause: Too many processes, not enough frames
CPU utilization drops

Solutions:
• Working Set Model: Keep frequently used pages
• Page Fault Frequency: Adjust frame allocation
• Reduce degree of multiprogramming
```

### Working Set Model
```
Working Set WS(t, Δ) = pages referenced in last Δ time units
Allocate frames based on working set size
If total working sets > available frames, suspend some process
```

---

# File Systems

## 1. File Allocation Methods

### 💡 Comparison
| Method | Sequential Access | Random Access | External Frag | Space Efficiency |
|--------|-------------------|---------------|---------------|------------------|
| Contiguous | Excellent | Good | Yes | Poor (need size) |
| Linked | Good | Poor (O(n)) | No | Overhead (pointers) |
| Indexed | Good | Good | No | Index block overhead |

### Contiguous Allocation
```
Each file occupies contiguous blocks
Directory: (start block, length)
Fast sequential and random access
External fragmentation
```

### Linked Allocation
```
Each block has pointer to next
Directory: (start block, end block)
No external fragmentation
Poor random access (must traverse)
```

### Indexed Allocation
```
Index block contains all block pointers
Directory: (index block number)
Good for random access
Overhead of index block

Multi-level for large files:
• Single-level index
• Multi-level index
• Combined (Unix inode)
```

---

## 2. Free Space Management

### 💡 Methods
```
Bit Vector (Bitmap):
• 1 bit per block (0 = free, 1 = used)
• Space: 1 bit per block
• Fast to find first free or n consecutive

Linked List:
• Free blocks linked together
• Space: 1 pointer per free block

Grouping:
• First free block stores addresses of n free blocks
• Last address points to another group
```

---

# Disk Scheduling

## 1. Disk Structure
```
Seek Time: Move head to correct cylinder (most significant)
Rotational Latency: Wait for sector to rotate under head
Transfer Time: Read/write data

Total Access Time = Seek + Rotation + Transfer
```

---

## 2. Disk Scheduling Algorithms

### 💡 Algorithm Comparison
| Algorithm | Description | Starvation |
|-----------|-------------|------------|
| FCFS | First come first serve | No |
| SSTF | Shortest seek time first | Yes |
| SCAN | Move in one direction, then reverse | No |
| C-SCAN | Move in one direction, jump back | No |
| LOOK | Like SCAN, but don't go to end | No |
| C-LOOK | Like C-SCAN, but don't go to end | No |

### 💡 Example
```
Request queue: 98, 183, 37, 122, 14, 124, 65, 67
Head starts at: 53
Disk range: 0-199

FCFS: 53→98→183→37→122→14→124→65→67
Total head movement = 640

SSTF: 53→65→67→37→14→98→122→124→183
Total head movement = 236

SCAN (going up): 53→65→67→98→122→124→183→199→37→14
Total head movement = 331

C-SCAN (going up): 53→65→67→98→122→124→183→199→0→14→37
Total head movement = 382

LOOK (going up): 53→65→67→98→122→124→183→37→14
Total head movement = 299
```

---

## Quick Memory Tricks 🧠

1. **Process states**: "New → Ready → Running → Waiting → Terminated"
2. **Deadlock conditions**: "MHNC" - Mutual exclusion, Hold & wait, No preemption, Circular wait
3. **Banker's**: "Need = Max - Allocation"
4. **Page faults**: FIFO can have Belady's anomaly
5. **LRU**: "Least Recently Used is removed"
6. **SCAN**: "Elevator algorithm"
7. **TLB**: Hit = 1 access, Miss = 2 accesses

---

## 💡 Quick Formulas

```
Turnaround Time = Completion - Arrival
Waiting Time = Turnaround - Burst
Response Time = First Response - Arrival

Page offset bits = log₂(page size)
Page number bits = address bits - offset bits
Number of pages = 2^(page number bits)

EAT = (1 - p) × mem_time + p × fault_time
    = hit_ratio × 1_access + miss_ratio × 2_accesses (for TLB)
```

---

## Common Mistakes to Avoid ⚠️

1. FCFS has convoy effect, not starvation
2. SJF is optimal for waiting time, not turnaround time
3. Banker's algorithm needs to check safety, not just availability
4. Paging has internal fragmentation, not external
5. TLB miss means 2 memory accesses, not just 1
6. FIFO page replacement can cause Belady's anomaly
7. LRU needs to track access history
8. SCAN goes to the end, LOOK doesn't
