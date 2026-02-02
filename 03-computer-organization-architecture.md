# 🖥️ Computer Organization & Architecture - Last Minute Notes

## Quick Navigation
- [Machine Instructions](#machine-instructions)
- [Addressing Modes](#addressing-modes)
- [CPU Design](#cpu-design)
- [Pipelining](#pipelining)
- [Memory Hierarchy](#memory-hierarchy)
- [Cache Memory](#cache-memory)
- [I/O Organization](#io-organization)

---

> **GATE Weightage**: ~5-8% (5-8 marks) | **Expected Questions**: 3-5

---

# Machine Instructions

## 1. Instruction Cycle

### 💡 Basic Instruction Cycle
```
Fetch → Decode → Execute → Memory Access → Write Back

1. Fetch: IR ← M[PC], PC ← PC + 1
2. Decode: Identify operation and operands
3. Execute: Perform ALU operation
4. Memory: Load/Store data
5. Write Back: Store result in register
```

### CPU Registers
| Register | Purpose |
|----------|---------|
| **PC** (Program Counter) | Address of next instruction |
| **IR** (Instruction Register) | Current instruction |
| **MAR** (Memory Address Register) | Address for memory access |
| **MBR/MDR** (Memory Buffer/Data Register) | Data for memory access |
| **AC** (Accumulator) | General purpose, stores results |
| **SP** (Stack Pointer) | Top of stack |

---

## 2. Instruction Formats

### 💡 Number of Bits Required
```
Opcode bits = ⌈log₂(number of operations)⌉
Register bits = ⌈log₂(number of registers)⌉
Address bits = ⌈log₂(memory size in words)⌉
```

### Instruction Types by Operand Count
| Type | Example | Description |
|------|---------|-------------|
| **3-Address** | ADD R1, R2, R3 | R1 ← R2 + R3 |
| **2-Address** | ADD R1, R2 | R1 ← R1 + R2 |
| **1-Address** | ADD R1 | AC ← AC + R1 |
| **0-Address** | ADD | Stack-based: TOS ← TOS + TOS-1 |

### Evaluation Example
Expression: X = (A + B) × (C + D)

**3-Address (4 instructions):**
```
ADD T1, A, B
ADD T2, C, D
MUL X, T1, T2
```

**2-Address (5 instructions):**
```
LOAD R1, A
ADD R1, B
LOAD R2, C
ADD R2, D
MUL R1, R2
STORE X, R1
```

**0-Address/Stack (7 instructions):**
```
PUSH A
PUSH B
ADD
PUSH C
PUSH D
ADD
MUL
POP X
```

---

# Addressing Modes

## 💡 Addressing Modes Summary

| Mode | Effective Address | Example | Use Case |
|------|-------------------|---------|----------|
| **Immediate** | Operand in instruction | ADD #5 | Constants |
| **Direct/Absolute** | EA = Address in instruction | ADD 1000 | Global variables |
| **Indirect** | EA = M[Address] | ADD (1000) | Pointers |
| **Register** | EA = Register | ADD R1 | Fast access |
| **Register Indirect** | EA = M[Register] | ADD (R1) | Array access |
| **Indexed** | EA = Base + Index | ADD 100(R1) | Arrays |
| **Base-Register** | EA = Base + Offset | ADD 100(BP) | Local variables |
| **PC-Relative** | EA = PC + Offset | JMP +50 | Branches |
| **Auto-increment** | EA = R, then R++ | ADD (R1)+ | Array traversal |
| **Auto-decrement** | R--, then EA = R | ADD -(R1) | Stack operations |

### Memory Access Count
```
Immediate: 0 memory access for operand
Direct: 1 memory access
Indirect: 2 memory accesses
Register: 0 memory access
Register Indirect: 1 memory access
```

---

# CPU Design

## 1. Control Unit Types

### Hardwired Control
```
+ Faster execution
+ Less hardware for simple instruction sets
- Complex to design and modify
- No flexibility

Used in: RISC processors
```

### Microprogrammed Control
```
+ Flexible, easy to modify
+ Supports complex instructions
- Slower (needs to fetch microinstructions)
- More memory required

Used in: CISC processors

Control Memory contains microinstructions
Microinstruction → Control signals
```

---

## 2. RISC vs CISC

### 💡 Comparison Table

| Feature | RISC | CISC |
|---------|------|------|
| Instructions | Simple, few | Complex, many |
| Instruction length | Fixed | Variable |
| Addressing modes | Few (typically 3-5) | Many (10-20) |
| Execution | Single cycle | Multi-cycle |
| Control | Hardwired | Microprogrammed |
| Registers | Many (32+) | Few (8-16) |
| Memory access | Load/Store only | Many instructions access memory |
| Pipelining | Easy | Complex |
| Compiler complexity | High | Low |
| Examples | ARM, MIPS, SPARC | x86, VAX |

---

# Pipelining

## 1. Basic Concepts

### 💡 5-Stage Pipeline (MIPS)
```
IF → ID → EX → MEM → WB

IF: Instruction Fetch
ID: Instruction Decode / Register Fetch
EX: Execute / Address Calculation
MEM: Memory Access
WB: Write Back
```

### Performance Formulas

**Pipeline Speedup:**
```
Speedup = Time(non-pipelined) / Time(pipelined)
Speedup = n × k / (k + n - 1)  [without stalls]

Where:
n = number of instructions
k = number of pipeline stages

Maximum speedup = k (when n → ∞)
```

**Pipeline Execution Time:**
```
Time = (k + n - 1) × cycle time

For n instructions in k-stage pipeline
First instruction: k cycles
Remaining (n-1): 1 cycle each
Total: k + (n-1) = k + n - 1 cycles
```

**Throughput:**
```
Throughput = n / ((k + n - 1) × cycle time)
Maximum throughput = 1 / cycle time  [when n → ∞]
```

---

## 2. Pipeline Hazards

### 💡 Types of Hazards

| Hazard Type | Cause | Solution |
|-------------|-------|----------|
| **Structural** | Resource conflict | Duplicate resources, stall |
| **Data** | Data dependency | Forwarding, stalling, reordering |
| **Control** | Branch instructions | Branch prediction, delayed branch |

### Data Hazards (RAW, WAR, WAW)
```
RAW (Read After Write) - True dependency:
  ADD R1, R2, R3    ; Writes R1
  SUB R4, R1, R5    ; Reads R1 ← Hazard!

WAR (Write After Read) - Anti-dependency:
  ADD R1, R2, R3    ; Reads R2
  SUB R2, R4, R5    ; Writes R2

WAW (Write After Write) - Output dependency:
  ADD R1, R2, R3    ; Writes R1
  SUB R1, R4, R5    ; Writes R1

Only RAW is true dependency in simple pipeline
```

### Data Hazard Solutions
```
1. Stalling (bubbles/NOPs): Insert wait cycles
   - Simple but reduces performance

2. Forwarding/Bypassing: 
   - Route result directly from ALU to next instruction
   - Eliminates most RAW hazards

3. Instruction Reordering:
   - Compiler rearranges instructions to avoid hazards
```

### 💡 Stall Cycles with Forwarding
```
Load-Use Hazard (needs 1 stall even with forwarding):
  LW R1, 100(R2)    ; Load R1
  ADD R3, R1, R4    ; Uses R1 ← 1 stall needed

Because: Load result available after MEM stage
         ADD needs it at EX stage
```

### Branch Hazard Solutions
```
1. Stall: Wait until branch resolved (waste cycles)

2. Branch Prediction:
   - Static: Always predict taken/not-taken
   - Dynamic: Use branch history table

3. Delayed Branch: 
   - Execute instruction after branch regardless
   - Compiler fills delay slot with useful instruction

4. Branch Target Buffer (BTB):
   - Cache for branch target addresses
```

---

## 3. Performance with Stalls

### 💡 CPI with Stalls
```
CPI = Ideal CPI + Stall cycles per instruction

For pipeline:
Ideal CPI = 1

CPI = 1 + (Stall frequency × Stall cycles)

Example:
30% loads, 50% of loads cause 1-cycle stall
Stall contribution = 0.30 × 0.50 × 1 = 0.15
CPI = 1 + 0.15 = 1.15
```

---

# Memory Hierarchy

## 1. Memory Types

### 💡 Memory Hierarchy (Top to Bottom)
```
           Cost/Bit  Speed    Size
Registers    Highest  Fastest  Smallest
    ↓
Cache (L1)
    ↓
Cache (L2/L3)
    ↓
Main Memory (RAM)
    ↓
Secondary (SSD/HDD)   Lowest   Slowest  Largest
```

### Memory Technologies
| Type | Persistence | Speed | Use |
|------|-------------|-------|-----|
| **SRAM** | Volatile | Fastest | Cache |
| **DRAM** | Volatile | Fast | Main memory |
| **Flash/SSD** | Non-volatile | Medium | Storage |
| **HDD** | Non-volatile | Slow | Storage |
| **ROM** | Non-volatile | Fast | Firmware |

### SRAM vs DRAM
| Feature | SRAM | DRAM |
|---------|------|------|
| Transistors/cell | 6 | 1 + capacitor |
| Speed | Faster | Slower |
| Cost | Higher | Lower |
| Refresh | Not needed | Needed |
| Density | Lower | Higher |

---

# Cache Memory

## 1. Cache Basics

### 💡 Key Formulas
```
Hit Rate = Hits / Total Accesses
Miss Rate = 1 - Hit Rate

Average Memory Access Time (AMAT):
AMAT = Hit Time + (Miss Rate × Miss Penalty)

For multi-level cache:
AMAT = L1_hit_time + L1_miss_rate × (L2_hit_time + L2_miss_rate × Memory_time)
```

### Cache Parameters
```
Cache Size = Number of blocks × Block size
Number of blocks = Cache Size / Block size

Tag bits = Address bits - Index bits - Block offset bits
Block offset bits = log₂(Block size)
```

---

## 2. Cache Mapping

### 💡 Mapping Comparison

| Mapping | Index Bits | Tag Bits | Comparators |
|---------|------------|----------|-------------|
| **Direct** | log₂(blocks) | High | 1 |
| **Fully Associative** | 0 | Highest | All blocks |
| **N-way Set Associative** | log₂(sets) | Medium | N |

### Direct Mapped Cache
```
Block address = Memory address / Block size
Cache block = Block address mod (Number of cache blocks)

Address: [Tag | Index | Block Offset]

Index bits = log₂(number of cache blocks)
Block offset = log₂(block size in bytes)
Tag = remaining bits
```

### Fully Associative Cache
```
Any block can go anywhere in cache
Address: [Tag | Block Offset]

+ No conflict misses
- Expensive (need to search all blocks)
```

### Set Associative Cache
```
Cache divided into sets, each set has N blocks (N-way)
Number of sets = Total blocks / N

Address: [Tag | Set Index | Block Offset]

Set index bits = log₂(number of sets)
```

### 💡 Quick Formula Reference
```
For cache with:
- S = number of sets
- E = associativity (blocks per set)  
- B = block size in bytes
- m = address bits

Cache Size = S × E × B bytes
Set index bits = log₂(S)
Block offset bits = log₂(B)
Tag bits = m - log₂(S) - log₂(B)
```

---

## 3. Cache Write Policies

### Write Hit Policies
| Policy | Description | Advantage |
|--------|-------------|-----------|
| **Write-Through** | Write to cache AND memory | Simple, memory always consistent |
| **Write-Back** | Write only to cache | Faster, less memory traffic |

### Write Miss Policies
| Policy | Description |
|--------|-------------|
| **Write-Allocate** | Bring block to cache, then write |
| **No-Write-Allocate** | Write directly to memory |

### 💡 Common Combinations
```
Write-through + No-write-allocate
Write-back + Write-allocate (most common)
```

---

## 4. Cache Replacement Policies

| Policy | Description | Implementation |
|--------|-------------|----------------|
| **LRU** | Replace least recently used | Optimal among practical |
| **FIFO** | Replace oldest block | Simple |
| **Random** | Random replacement | Simplest |
| **LFU** | Replace least frequently used | Complex |

---

## 5. Types of Cache Misses (3 Cs)

```
1. Compulsory (Cold) Miss:
   - First access to a block
   - Cannot be avoided

2. Capacity Miss:
   - Cache too small
   - Increase cache size

3. Conflict Miss:
   - Multiple blocks map to same set
   - Increase associativity
```

---

# I/O Organization

## 1. I/O Techniques

### 💡 Comparison

| Method | CPU Involvement | Speed | Use Case |
|--------|-----------------|-------|----------|
| **Programmed I/O** | High (polling) | Slow | Simple devices |
| **Interrupt-driven** | Medium | Medium | General purpose |
| **DMA** | Low | Fast | High-speed, bulk transfer |

### Programmed I/O
```
CPU continuously checks device status (polling)
+ Simple
- CPU wastes time waiting
```

### Interrupt-driven I/O
```
Device interrupts CPU when ready
+ CPU can do other work
- Overhead per interrupt
```

### DMA (Direct Memory Access)
```
DMA controller handles transfer directly
+ Minimal CPU involvement
+ High-speed bulk transfers
- Additional hardware

DMA modes:
1. Burst mode: DMA takes bus until done
2. Cycle stealing: DMA takes 1 cycle at a time
3. Interleaved: Alternate between CPU and DMA
```

---

## 2. Bus Architecture

### Bus Types
```
Data Bus: Carries data (bidirectional)
Address Bus: Carries addresses (unidirectional)
Control Bus: Carries control signals

Bus width = Number of bits transferred in parallel
```

### Synchronous vs Asynchronous Bus
| Synchronous | Asynchronous |
|-------------|--------------|
| Clock-based | Handshaking |
| Faster | Flexible |
| All devices same speed | Different speed devices OK |

---

## 3. Interrupts

### Interrupt Types
```
1. Hardware Interrupt: From external devices
2. Software Interrupt: From programs (TRAP, syscall)
3. Exception: From CPU (divide by zero, page fault)
```

### Interrupt Handling
```
1. Complete current instruction
2. Save PC and status registers
3. Identify interrupt source
4. Jump to ISR (Interrupt Service Routine)
5. Execute ISR
6. Restore registers
7. Return to interrupted program
```

### Interrupt Priority
```
Multiple interrupts: Handle highest priority first
Nested interrupts: Higher priority can interrupt lower
```

---

## Quick Memory Tricks 🧠

1. **Pipeline speedup**: Max = number of stages (k)
2. **RAW hazard**: "Read needs Write's result"
3. **Cache 3 Cs**: "Compulsory, Capacity, Conflict"
4. **AMAT**: "Hit time + Miss rate × Miss penalty"
5. **SRAM vs DRAM**: "SRAM = 6T, Static, Cache; DRAM = 1T+C, Dynamic, RAM"
6. **Write-back**: "Lazy write, dirty bit"
7. **DMA**: "CPU gets bus after transfer"

---

## Common Mistakes to Avoid ⚠️

1. Forgetting pipeline creates k + n - 1 cycles, not k × n
2. Wrong tag/index/offset bit calculation for cache
3. Confusing write-through with write-back
4. Forgetting load-use hazard needs stall even with forwarding
5. AMAT calculation: forgetting to multiply miss rate by penalty
6. Confusing structural hazard (resource) with data hazard (dependency)
7. Wrong speedup formula (non-pipelined time / pipelined time)

---

## 📝 GATE Previous Year Patterns

### Most Frequently Asked Topics
1. **Cache Mapping & AMAT** - 2-3 questions/year
2. **Pipeline Speedup & Hazards** - 2 questions/year
3. **Addressing Modes** - 1 question/year
4. **Instruction Formats** - 1 question/year
5. **DMA & I/O** - 1 question/year

### 💡 GATE-Style Practice Problems

**Problem 1 (Cache - GATE Pattern):**
```
A 2-way set associative cache has 256 KB total size with 64-byte 
block size. For a 32-bit address, find tag, index, and offset bits.

Solution:
Block size = 64B = 2^6 → Offset bits = 6
Total blocks = 256KB / 64B = 4096 blocks
Sets = 4096 / 2 = 2048 sets = 2^11 → Index bits = 11
Tag bits = 32 - 11 - 6 = 15 bits ✓

Address format: [Tag: 15 | Index: 11 | Offset: 6]
```

**Problem 2 (AMAT - GATE Pattern):**
```
L1 cache: hit time = 1 cycle, hit rate = 90%
L2 cache: access time = 10 cycles, hit rate = 80%
Memory: access time = 100 cycles
Calculate AMAT.

Solution:
AMAT = L1_hit_time + L1_miss_rate × (L2_time + L2_miss_rate × Mem_time)
AMAT = 1 + 0.1 × (10 + 0.2 × 100)
AMAT = 1 + 0.1 × (10 + 20)
AMAT = 1 + 0.1 × 30 = 1 + 3 = 4 cycles ✓
```

**Problem 3 (Pipeline - GATE Pattern):**
```
A 5-stage pipeline has:
- 20% branches with 2-cycle penalty
- 30% loads with 1-cycle stall (data hazard)
Calculate effective CPI.

Solution:
CPI = Ideal CPI + Branch stalls + Data stalls
CPI = 1 + (0.20 × 2) + (0.30 × 1)
CPI = 1 + 0.4 + 0.3 = 1.7 ✓
```

**Problem 4 (Pipeline Speedup - GATE Pattern):**
```
Execute 100 instructions on a 5-stage pipeline. Each stage takes 2 ns.
Compare with non-pipelined execution.

Solution:
Non-pipelined: 100 × 5 × 2 = 1000 ns
Pipelined: (5 + 100 - 1) × 2 = 104 × 2 = 208 ns
Speedup = 1000 / 208 = 4.81 ✓

Maximum speedup = k = 5 (as n → ∞)
```

**Problem 5 (Cache Mapping - GATE Pattern):**
```
Direct mapped cache with 8 blocks, block size 4 words.
Word address 29 maps to which cache block?

Solution:
Block address = Word address / Block size = 29 / 4 = 7
Cache block = Block address mod Number of blocks = 7 mod 8 = 7 ✓
```

**Problem 6 (Addressing Mode - GATE Pattern):**
```
Instruction: ADD R1, (R2)+
R2 = 1000, Memory[1000] = 50, R1 = 25
After execution, what are R1 and R2?

Solution:
This is auto-increment addressing.
1. Effective address = R2 = 1000
2. Operand = Memory[1000] = 50
3. R1 = R1 + 50 = 25 + 50 = 75
4. R2 = R2 + 4 = 1004 (assuming word size = 4)

R1 = 75, R2 = 1004 ✓
```

**Problem 7 (Virtual Memory - GATE Pattern):**
```
32-bit virtual address, 4KB page size, 4-byte page table entry.
Calculate page table size.

Solution:
Page offset = log₂(4KB) = 12 bits
Page number bits = 32 - 12 = 20 bits
Number of pages = 2^20 = 1M pages
Page table size = 1M × 4 bytes = 4 MB ✓
```

---

## 📊 Formula Quick Reference Sheet

### Cache Formulas
```
Block offset bits = log₂(block size)
Index bits = log₂(number of sets)
Tag bits = Address bits - Index bits - Offset bits
Number of sets = Total blocks / Associativity
Cache size = Number of sets × Associativity × Block size

AMAT = Hit time + Miss rate × Miss penalty
Hit rate = 1 - Miss rate
```

### Pipeline Formulas
```
Execution time = (k + n - 1) × cycle time
Speedup = k × n / (k + n - 1)
Maximum speedup = k (number of stages)
Throughput = n / ((k + n - 1) × cycle time)
CPI = 1 + Stall cycles per instruction
```

### Memory Formulas
```
Page table entries = 2^(page number bits)
Page table size = Entries × Entry size
Number of pages = Virtual address space / Page size
Number of frames = Physical memory / Page size
```

### DMA and I/O
```
DMA transfer time = Setup time + (Data size / Bandwidth)
Interrupt overhead = Context switch time × Number of interrupts
Polling efficiency depends on polling frequency vs event frequency
```

### Instruction Format
```
Opcode bits = ⌈log₂(number of operations)⌉
Register bits = ⌈log₂(number of registers)⌉
Address bits = ⌈log₂(memory size in words)⌉
```
