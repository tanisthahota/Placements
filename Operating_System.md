# Operating Systems - Comprehensive Notes

## What is an Operating System?

*Definition*: An Operating System is system software that manages computer hardware, software resources, and provides common services for computer programs.

A *manager* that coordinates between applications and the computer's resources (CPU, memory, storage, devices).

*Key Functions*:
- *Resource Management*: CPU, memory, storage, I/O devices
- *Process Management*: Running and controlling programs
- *File System Management*: Organizing and accessing files
- *Security*: Protecting system and user data
- *User Interface*: Command line or graphical interface

### What happens if there is no OS?
- Resource exploitation - 1 App will use all the resources 
- Memory has no protection
- Bulky and complex app - hardware interaction code must be in app's code base

*OS Goals*:
- Maximum CPU utilization
- Less process starvation  
- Higher priority job execution

## Types of Operating Systems

### Single Process OS
Only 1 process executes at a time from ready queue. Oldest type.

### Batch Processing OS
*Process*:
1. User prepares job using punch cards
2. Submits job to computer operator  
3. Operator sorts jobs into batches with similar needs
4. Batches executed one by one

*Problems*:
- No priority setting
- May lead to starvation
- CPU idle during I/O operations

### Multiprogramming OS
- Increases CPU utilization by keeping multiple jobs in memory
- Single CPU with context switching
- Switch happens when process goes to wait state
- Examples: THE (Dijkstra, early 1960s)

### Multitasking OS  
- Logical extension of multiprogramming
- Single CPU runs multiple tasks simultaneously
- Uses context switching and time sharing
- Examples: CTSS (MIT, early 1960s)

### Multi-processing OS
- More than 1 CPU in single computer
- Better reliability and throughput
- Less process starvation
- Examples: Windows NT

### Distributed OS
- Manages resources across multiple networked nodes
- Loosely connected autonomous systems
- Examples: LOCUS

### Real-Time OS (RTOS)
- Error-free computations within tight time boundaries
- Used in Air Traffic Control, Robots
- Examples: ATCS

## Multi-Tasking vs Multi-Threading

| Multi-Tasking | Multi-Threading |
|---------------|-----------------|
| More than one task simultaneously | Process divided into sub-tasks (threads) |
| Multiple processes context switched | Multiple threads context switched |
| No. of CPU = 1 | No. of CPU ≥ 1 (better performance) |
| Isolation and memory protection exists | No isolation, resources shared among threads |

## Core OS Components

### 1. Kernel
Core part of OS that directly interacts with hardware

*Functions*:
- Process scheduling and management
- Memory management  
- File management
- I/O management and device drivers
- System calls and interrupt handling

*Types of Kernels*:

**Monolithic Kernel**
- All functions in kernel itself
- *Pros*: High performance, fast communication
- *Cons*: Bulky, less reliable, high memory usage
- *Examples*: Linux, Unix, MS-DOS

**Micro Kernel**  
- Only major functions in kernel (Memory, Process mgmt)
- File and I/O mgmt in user space
- *Pros*: Smaller, more reliable and stable
- *Cons*: Slower performance, mode switching overhead
- *Examples*: MINIX, L4 Linux, Symbian OS

**Hybrid Kernel**
- Combined approach
- Speed of monolithic + modularity of micro
- *Examples*: macOS, Windows NT/7/10

### 2. User Space
Where application software runs without privileged hardware access

*Types*:
- *GUI*: Graphical User Interface
- *CLI*: Command Line Interface

### 3. Shell
Interface between user and kernel (command interpreter)

*Communication*: User mode ↔ Kernel mode via Inter Process Communication (IPC)

## System Calls

*How apps interact with Kernel*: Using system calls

*Example*: `mkdir laks`
- mkdir calls kernel's file management module
- mkdir is wrapper around actual system calls
- Transitions via software interrupts

*System Call Process*:
1. User executes process (User Space)
2. Gets system call (User Space)
3. Exec system call (Kernel Space)
4. Return to User Space

### Types of System Calls

**1. Process Control**
- end, abort, load, execute
- create/terminate process
- get/set process attributes
- wait operations, memory allocation

**2. File Management**  
- create/delete file
- open, close, read, write
- get/set file attributes

**3. Device Management**
- request/release device
- read/write operations
- get/set device attributes

**4. Information Maintenance**
- get/set time, date, system data
- get/set attributes

**5. Communication Management**
- create/delete connections
- send/receive messages
- status transfers

*Examples*:

| Category | Windows | Unix |
|----------|---------|------|
| Process Control | CreateProcess(), ExitProcess() | fork(), exit(), wait() |
| File Management | CreateFile(), ReadFile() | open(), read(), write() |
| Device Management | ReadConsole(), WriteConsole() | ioctl(), read(), write() |

## Boot Process

*What happens when you turn on computer?*

1. **PC Power On** → CPU initializes
2. **BIOS/UEFI Loading** → CPU loads firmware from BIOS chip  
3. **POST Process** → Power On Self-Test, hardware initialization
4. **Bootloader** → BIOS loads bootloader from MBR (Master Boot Record)
5. **OS Loading** → Bootloader loads actual OS (Kernel then User Space)

*Bootloaders*:
- Windows: Windows Boot Manager (Bootmgr.exe)
- Linux: GRUB
- macOS: boot.efi

## 32-Bit vs 64-Bit OS

| Aspect | 32-bit | 64-bit |
|--------|--------|--------|
| *Registers* | 32-bit registers | 64-bit registers |
| *Memory* | 2³² addresses (4GB max) | 2⁶⁴ addresses (massive capacity) |
| *Performance* | 4 bytes per instruction | 8 bytes per instruction |
| *Compatibility* | Only 32-bit OS | Both 32-bit and 64-bit OS |

*Advantages of 64-bit*:
- Much larger memory addressing
- Better performance for calculations
- Enhanced graphics performance
- Backward compatibility with 32-bit

## Storage Devices & Memory Hierarchy

*Memory Types*:

1. **Registers**: Smallest, fastest, most expensive (part of CPU)
2. **Cache**: L1, L2, L3 levels for frequently used data  
3. **Main Memory (RAM)**: Primary memory for active processes
4. **Secondary Storage**: HDD/SSD for permanent storage

*Comparison*:

| Aspect | Primary Storage | Secondary Storage |
|--------|----------------|-------------------|
| *Cost* | Expensive | Cheaper |
| *Speed* | High | Lower |  
| *Size* | Small | Large |
| *Volatility* | Volatile | Non-volatile |

## Process Management

### What is a Process?
*Program*: Compiled code ready to execute (stored on disk)
*Process*: Program under execution (resides in RAM)
*Thread*: Single sequence stream within process, lightweight execution unit

### How OS Creates Process
*Steps*:
1. Load program and static data into memory
2. Allocate runtime stack  
3. Heap memory allocation
4. I/O task setup
5. OS handoffs control to main()

### Process Architecture
- *Text Section*: Program code
- *Stack*: Temporary data, function parameters
- *Heap*: Dynamically allocated memory
- *Data Section*: Global variables

### Process Attributes (PCB - Process Control Block)
*PCB stores*:
- Process ID (PID)
- Process state
- Program counter
- CPU registers
- Memory management info
- I/O status
- Scheduling information

### Process States

New → Ready → Running → Waiting → Terminated

1. *New*: Process being created
2. *Ready*: Waiting for CPU assignment  
3. *Running*: Instructions being executed
4. *Waiting*: Waiting for I/O or event
5. *Terminated*: Execution completed

### Process Queues

**Job Queue**: Processes in New state (secondary memory)
- *Job Scheduler (LTS)*: Picks processes and loads into memory

**Ready Queue**: Processes in Ready state (main memory)  
- *CPU Scheduler (STS)*: Picks process and dispatches to CPU

**Waiting Queue**: Processes in Wait state

*Degree of Multiprogramming*: Number of processes in memory (controlled by LTS)

*Dispatcher*: Module that gives CPU control to selected process

### Important Process Concepts

**Swapping**
- Medium Term Scheduler (MTS) removes processes from memory
- Swap-out and swap-in to manage memory
- Process execution continues where it left off

**Context Switching**  
- Save current process state in PCB
- Load new process state from PCB
- Pure overhead but necessary for multiprogramming

**Orphan Process**
- Process whose parent terminated but it's still running
- Adopted by init process (first OS process)

**Zombie Process**
- Process execution completed but entry remains in process table
- Parent hasn't read exit status yet
- Removed after parent calls wait()

## CPU Scheduling

*Purpose*: By switching CPU among processes, OS makes computer more productive

### Goals of CPU Scheduling
- Maximum CPU utilization
- Minimum Turnaround Time (TAT)
- Minimum Wait Time  
- Minimum Response Time
- Maximum system throughput

### Key Metrics
- *Arrival Time (AT)*: When process enters ready queue
- *Burst Time (BT)*: Time required for execution
- *Completion Time (CT)*: When process terminates
- *Turnaround Time (TAT)*: CT - AT
- *Wait Time (WT)*: TAT - BT  
- *Response Time*: Time from ready queue to first CPU allocation
- *Throughput*: Processes completed per unit time

### Preemptive vs Non-Preemptive

**Non-Preemptive**
- Process keeps CPU until termination or wait state
- *Problems*: Starvation, low CPU utilization

**Preemptive**  
- CPU taken away after time quantum expires
- *Benefits*: Less starvation, high CPU utilization

### CPU Scheduling Algorithms

**1. First Come First Serve (FCFS)**
- *Logic*: Execute in arrival order
- *Pros*: Simple, fair
- *Cons*: Convoy Effect (long process blocks shorter ones)
- *Use case*: Batch systems

**2. Shortest Job First (SJF)**

*Non-preemptive*:
- Execute shortest burst time first
- *Pros*: Optimal average wait time
- *Cons*: Starvation, estimation needed

*Preemptive (SRTF)*:
- Preempt if shorter job arrives
- Less starvation, no convoy effect

**3. Priority Scheduling**

*Non-preemptive*: Run highest priority to completion
*Preemptive*: Preempt if higher priority arrives

*Problem*: Indefinite waiting (starvation)
*Solution*: Aging - gradually increase priority

**4. Round Robin (RR)**
- *Logic*: Each process gets fixed time quantum
- *Pros*: Fair, good response time, no starvation
- *Cons*: Context switching overhead
- *Use case*: Time-sharing systems

*Performance depends on time quantum*:
- Too small: High overhead
- Too large: Becomes FCFS

**5. Multi-Level Queue (MLQ)**
- Ready queue divided into multiple sub-queues
- Process permanently assigned based on type:
  - System processes (highest priority)
  - Interactive processes  
  - Batch processes (lowest priority)
- Each queue has own scheduling algorithm
- *Problem*: Starvation of lower priority queues

**6. Multi-Level Feedback Queue (MLFQ)**
- Processes can move between queues
- Separates processes by burst time characteristics
- I/O bound processes stay in higher priority
- CPU bound processes move to lower priority
- *Benefits*: Less starvation, flexible, aging prevents starvation

### Scheduling Algorithm Comparison

| Algorithm | Design | Preemption | Convoy Effect | Starvation |
|-----------|--------|------------|---------------|------------|
| FCFS | Simple | No | Yes | Possible |
| SJF | Complex | No | Yes | Yes |
| SRTF | Complex | Yes | No | Possible |
| Priority | Complex | Optional | Depends | Yes |
| RR | Simple | Yes | No | No |
| MLQ | Complex | Yes | Yes | Yes |
| MLFQ | Complex | Yes | Possible | Less |

## Concurrency & Threading

### Thread Characteristics
- Single sequence stream within process
- Independent execution path
- Lightweight process
- Used for parallelism within process
- *Example*: Browser tabs, text editor (typing, spell-check, save)

### Thread Scheduling
Threads scheduled based on priority with CPU time slices

### Thread Context Switching
- Save/restore thread state (not memory address space)
- Faster than process switching
- CPU cache state preserved
- Uses TCB (Thread Control Block)

### Benefits of Multi-Threading
- *Responsiveness*: Better user interaction
- *Resource Sharing*: Efficient sharing within process
- *Economy*: Cheaper to create than processes
- *Multiprocessor Utilization*: True parallelism on multiple CPUs

*Note*: Single CPU systems don't gain from multi-threading due to context switching overhead

## Memory Management

### Logical vs Physical Address

**Logical Address**:
- Generated by CPU (Virtual Address)
- Range: 0 to max
- User accessible
- Doesn't exist physically

**Physical Address**:
- Actual memory location
- Range: (R + 0) to (R + max) for base R
- Computed by MMU (Memory Management Unit)
- User has indirect access only

### Memory Protection & Isolation
- *Relocation Register*: Base address
- *Limit Register*: Range of logical addresses  
- Every logical address checked against limit
- MMU maps logical to physical by adding base

### Memory Allocation Methods

#### Contiguous Memory Allocation

**Fixed Partitioning**
- Memory divided into fixed-size partitions
- *Problems*:
  - *Internal Fragmentation*: Unused partition space
  - *External Fragmentation*: Total free space non-contiguous
  - Process size limitation
  - Low degree of multiprogramming

**Dynamic Partitioning**
- Partition size determined at process loading
- *Advantages*: No internal fragmentation, no process size limit
- *Problem*: External fragmentation

#### Free Space Management

**Defragmentation/Compaction**
- Make all free partitions contiguous
- Merge scattered free spaces
- *Drawback*: System efficiency decreases during compaction

**Allocation Algorithms**:

*First Fit*: Allocate first sufficient hole
- *Pros*: Fast, simple
- *Cons*: May waste space

*Best Fit*: Allocate smallest sufficient hole  
- *Pros*: Less internal fragmentation
- *Cons*: Creates small holes, slow

*Worst Fit*: Allocate largest hole
- *Pros*: Leaves larger remaining holes
- *Cons*: Slow, wasteful

*Next Fit*: First fit starting from last allocation
- Similar to First Fit but different starting point

#### Non-Contiguous Memory Allocation

**Paging**
- *Concept*: Divide memory into fixed-size blocks
- *Pages*: Logical memory blocks
- *Frames*: Physical memory blocks  
- Page size = Frame size

*Benefits*:
- No external fragmentation
- No need for compaction
- Allows non-contiguous allocation

*Page Table*: Maps pages to frames
- Stored in main memory
- PTBR (Page Table Base Register) points to current table

*Address Translation*:
Logical Address = Page Number + Page Offset
Physical Address = Frame Number + Page Offset

*Translation Lookaside Buffer (TLB)*:
- Hardware cache for page table entries
- Speeds up address translation
- Contains recent page-to-frame mappings
- Uses ASID (Address Space Identifiers) for process protection

**Segmentation**
- *Concept*: Divide process based on logical units
- User view of memory (code, data, stack segments)
- Variable segment sizes
- Address: <segment-number, offset>

*Advantages*:
- No internal fragmentation
- Efficient intra-segment operations
- Smaller segment table than page table
- Better compiler organization

*Disadvantages*:
- External fragmentation
- Complex swapping due to variable sizes

*Modern systems use hybrid approach combining paging and segmentation*

## Virtual Memory

### Concept
Technique allowing execution of processes not completely in memory. Provides illusion of very large main memory using secondary storage.

### Benefits
- Programs can be larger than physical memory
- More programs can run simultaneously  
- Better CPU utilization and throughput

### Demand Paging
Popular virtual memory implementation

*How it works*:
1. Lazy swapper brings pages only when needed
2. Valid-invalid bit in page table:
   - 1: Page in memory and valid
   - 0: Page on disk or invalid
3. Page fault occurs when accessing invalid page

*Page Fault Handling*:
1. Check if reference was valid (using PCB)
2. If invalid → terminate process
3. If valid → find free frame
4. Schedule disk read to load page
5. Update page table
6. Restart interrupted instruction

*Pure Demand Paging*: Start process with no pages in memory

### Page Replacement Algorithms
When all frames occupied, must replace page for new page

**1. FIFO (First In First Out)**
- Replace oldest page
- *Pros*: Simple to implement
- *Cons*: Poor performance, Belady's Anomaly
- *Belady's Anomaly*: More frames can increase page faults

**2. Optimal Page Replacement**
- Replace page referenced farthest in future
- *Pros*: Lowest page fault rate
- *Cons*: Impossible to implement (requires future knowledge)

**3. LRU (Least Recently Used)**
- Replace page unused for longest time
- *Implementation*:
  - *Counters*: Time stamp each page access
  - *Stack*: Maintain stack of page numbers

**4. Counting-Based Algorithms**
- *LFU (Least Frequently Used)*: Replace page with smallest reference count
- *MFU (Most Frequently Used)*: Replace page with largest reference count
- Neither commonly used

### Thrashing
*Problem*: System spends more time paging than executing

*Cause*: Process doesn't have enough frames for working set

*Solutions*:
- *Working Set Model*: Allocate frames based on locality
- *Page Fault Frequency*: Control page fault rate with upper/lower bounds
- Reduce degree of multiprogramming

## Synchronization

### Critical Section Problem
*Problem*: Multiple processes accessing shared resources simultaneously can cause inconsistent results

*Race Condition*: Result depends on timing of process execution

### Requirements for Solution
1. *Mutual Exclusion*: Only one process in critical section
2. *Progress*: Selection cannot be postponed indefinitely  
3. *Bounded Waiting*: Limited waiting time

### Synchronization Tools

#### 1. Mutex (Mutual Exclusion)
```
mutex_lock(&lock);
// Critical Section
mutex_unlock(&lock);
```

*Problems*:
- Contention and busy waiting
- Deadlock possibility
- Debugging complexity
- Priority inversion

#### 2. Conditional Variables
- Synchronization primitive for waiting until condition occurs
- Works with mutex lock
- Avoids busy waiting
- Thread waits → releases lock → waits for notification

#### 3. Semaphores
*Definition*: Integer variable equal to number of available resources

*Types*:
- *Binary Semaphore*: 0 or 1 (like mutex)
- *Counting Semaphore*: Can be > 1

*Operations*:
- *wait()*: Decrement semaphore (P operation)
- *signal()*: Increment semaphore (V operation)

*Implementation*: Use waiting queue instead of busy waiting

#### Classic Synchronization Problems

**1. Producer-Consumer Problem**
```
semaphore empty = n;    // Empty slots
semaphore full = 0;     // Full slots  
semaphore mutex = 1;    // Critical section

Producer:
    wait(empty);
    wait(mutex);
    // Add item to buffer
    signal(mutex);
    signal(full);

Consumer:
    wait(full);
    wait(mutex);
    // Remove item from buffer
    signal(mutex);
    signal(empty);
```

**2. Dining Philosophers Problem**
*Setup*: 5 philosophers, 5 chopsticks, need 2 to eat

*Problem*: Deadlock if all pick left chopstick simultaneously

*Solutions*:
- Allow maximum 4 philosophers at table
- Pick both chopsticks atomically
- Odd-even rule: odd picks left first, even picks right first

## Deadlock

### Definition
Two or more processes waiting indefinitely for resources held by each other

### Necessary Conditions (Coffman Conditions)
All four must hold simultaneously:

1. *Mutual Exclusion*: Resources cannot be shared
2. *Hold and Wait*: Process holds resources while waiting for more
3. *No Preemption*: Resources cannot be forcibly taken
4. *Circular Wait*: Circular chain of waiting processes

### Methods for Handling Deadlocks

#### 1. Deadlock Prevention
Ensure at least one necessary condition cannot hold

*Prevent Mutual Exclusion*: Make resources sharable (limited applicability)

*Prevent Hold and Wait*:
- Protocol A: Request all resources before execution
- Protocol B: Release all resources before requesting new ones

*Allow Preemption*:
- Preempt resources from waiting processes
- May cause livelock

*Prevent Circular Wait*:
- Impose ordering on resource allocation
- All processes request resources in same order

#### 2. Deadlock Avoidance
System decides whether to grant resource request based on future safety

*Safe State*: System can allocate resources to each process without deadlock
*Unsafe State*: May lead to deadlock (but not necessarily)

*Banker's Algorithm*: Check if granting request leaves system in safe state

#### 3. Deadlock Detection and Recovery
Allow deadlocks, then detect and recover

*Detection*:
- Single instance: Wait-for graph, look for cycles
- Multiple instances: Use resource allocation matrices

*Recovery*:
- *Process Termination*: Abort all deadlocked processes or one at a time
- *Resource Preemption*: Take resources from processes

#### 4. Deadlock Ignorance (Ostrich Algorithm)
Pretend deadlocks don't occur (used by many systems)

## File Systems

### File Operations
- *Create*: Make new file
- *Open*: Prepare for access  
- *Read*: Get data from file
- *Write*: Put data to file
- *Seek*: Change current position
- *Close*: Finish access
- *Delete*: Remove file

### Directory Structure
*Single-level*: All files in one directory
*Two-level*: User directories under root  
*Tree*: Hierarchical structure (most common)
*Graph*: Allows links and shortcuts

### File Allocation Methods

#### 1. Contiguous Allocation
- Store files in consecutive blocks
- *Pros*: Fast access, simple implementation
- *Cons*: External fragmentation, difficult to grow files

#### 2. Linked Allocation  
- Each block points to next block
- *Pros*: No fragmentation, easy to grow
- *Cons*: Sequential access only, pointer overhead

#### 3. Indexed Allocation
- Index block contains pointers to data blocks  
- *Pros*: Direct access, no fragmentation
- *Cons*: Index block overhead

### Modern File Systems
- *NTFS* (Windows): Journaling, compression, encryption
- *ext4* (Linux): Journaling, large file support
- *APFS* (macOS): Copy-on-write, snapshots
- *ZFS*: Advanced features, data integrity

## I/O Systems

### I/O Hardware
- *I/O Ports*: Communication endpoints
- *Buses*: Data pathways (PCI, USB, SATA)
- *Controllers*: Hardware managing devices

### I/O Methods

#### 1. Programmed I/O (Polling)
- CPU constantly checks device status
- *Pros*: Simple
- *Cons*: CPU waste, poor performance

#### 2. Interrupt-Driven I/O
- Device sends interrupt when ready
- *Pros*: CPU can do other work
- *Cons*: High overhead for bulk transfers

#### 3. Direct Memory Access (DMA)
- Device transfers data directly to/from memory
- *Pros*: Minimal CPU involvement
- *Cons*: More complex hardware

### I/O Scheduling
*Purpose*: Optimize disk access patterns

*Algorithms*:
- *FCFS*: First come, first served
- *SCAN*: Elevator algorithm
- *C-SCAN*: Circular SCAN  
- *LOOK*: SCAN but only go as far as needed

## Security and Protection

### Security Goals
- *Confidentiality*: Prevent unauthorized disclosure
- *Integrity*: Prevent unauthorized modification
- *Availability*: Ensure authorized access

### Protection Mechanisms
- *Access Control Lists (ACL)*: Permissions per object
- *Capability Lists*: Permissions per user
- *Role-Based Access Control (RBAC)*: Permissions by role

### Authentication Methods
- *Something you know*: Passwords, PINs
- *Something you have*: Smart cards, tokens  
- *Something you are*: Biometrics

## Key Interview Questions

### Q: What's the difference between process and thread?
*Process*: Independent program with own memory space, expensive to create/switch
*Thread*: Lightweight execution unit within process, shares memory, cheaper to create/switch
*Example*: Browser (process) with multiple tabs (threads)

### Q: Explain virtual memory
Virtual memory allows programs larger than physical RAM by using disk as extension. Pages loaded on demand, least recently used pages swapped out. Provides illusion of unlimited memory.

### Q: What causes thrashing and how to prevent it?
*Cause*: System spends more time swapping than executing due to too many processes
*Prevention*: Reduce multiprogramming, increase memory, improve page replacement, use working set model

### Q: Difference between preemptive and non-preemptive scheduling?
*Preemptive*: OS can interrupt running process (RR, Priority)
*Non-preemptive*: Process runs until completion (FCFS, SJF)
*Trade-off*: Preemptive gives better response time but higher overhead

### Q: How does paging work?
Paging divides memory into fixed blocks. Page table maps logical pages to physical frames. CPU generates logical address, MMU translates using page table. TLB caches translations for speed.

### Q: Explain the producer-consumer problem
Producer creates data, consumer uses it. 

Problems: buffer overflow/underflow. Solution: Use semaphores - empty tracks free slots, full tracks occupied slots, mutex protects critical section.