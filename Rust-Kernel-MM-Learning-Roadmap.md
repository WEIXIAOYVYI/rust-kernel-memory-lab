# Rust Kernel Memory Management Learning Roadmap

## 总体目标

通过学习、设计和实验，形成一套 Rust Kernel Memory Management
子系统设计能力。

核心路径：

Problem → Model → Invariant → Reference → Design → Implement → Validate

------------------------------------------------------------------------

# Phase 0: Memory Model（建立内存心智模型）

## 目标

理解：

-   为什么需要 Memory Management
-   Virtual Address / Physical Address
-   Page / Frame
-   Mapping
-   MMU 和地址转换

## 学习主题

### 0.1 Why Memory Management

问题：

-   程序为什么不能直接访问物理内存？
-   虚拟内存解决什么问题？

产出：

-   why-mm.md

### 0.2 Address Model

理解：

-   PhysAddr
-   VirtAddr
-   Address Space
-   Alignment

产出：

-   address-model.md

### 0.3 Page & Frame

理解：

-   Page
-   Frame
-   PFN
-   VPN
-   Offset

核心：

Page != Frame

产出：

-   page-frame-model.md

### 0.4 Mapping Model

理解：

-   VA 到 PA 的关系
-   Permission
-   Valid bit
-   Dirty bit

产出：

-   mapping-model.md

### 0.5 MMU Hardware

AArch64:

-   TTBR
-   TCR
-   MAIR
-   PTE
-   TLB

x86:

-   CR3
-   Page Table Level
-   PTE

产出：

-   mmu.md

完成标准：

能够解释：

-   malloc 和物理内存的关系
-   page table 为什么存在
-   page fault 为什么是正常机制

------------------------------------------------------------------------

# Phase 1: Physical Memory Management

## 目标

理解：

OS 如何管理真实 RAM。

## 学习主题

### 1.1 Memory Discovery

学习：

-   UEFI memory map
-   Device Tree memory

设计：

MemoryRegion

------------------------------------------------------------------------

### 1.2 Frame Abstraction

研究：

-   xv6 kalloc
-   Linux struct page
-   Rust OS Frame abstraction

关注：

-   Ownership
-   Lifetime

产出：

frame-abstraction.md

------------------------------------------------------------------------

### 1.3 Physical Allocator

学习：

阶段：

1.  Bitmap allocator
2.  Free List
3.  Buddy allocator

参考：

-   xv6
-   Linux buddy

产出：

frame-allocator-design.md

------------------------------------------------------------------------

### 1.4 Linux Buddy Analysis

理解：

-   Zone
-   Node
-   Order
-   Migratetype

目标：

理解 Linux 复杂性的来源。

完成标准：

实现：

-   allocate frame
-   release frame
-   memory statistics

------------------------------------------------------------------------

# Phase 2: Page Table & Virtual Memory

## 目标

设计虚拟内存系统。

## 学习主题

### 2.1 Page Table

理解：

-   Page Table Level
-   PTE
-   Mapping Flags

设计：

PageTable abstraction

------------------------------------------------------------------------

### 2.2 Address Space

研究：

-   Linux mm_struct
-   xv6 pagetable

设计：

AddressSpace

------------------------------------------------------------------------

### 2.3 VMA

理解：

Page Table:

当前映射

VMA:

应该是什么

产出：

vma-design.md

------------------------------------------------------------------------

### 2.4 Page Fault

流程：

CPU → Fault → Kernel → Find Region → Allocate Frame → Map

产出：

page-fault-design.md

完成标准：

支持：

-   用户地址空间
-   lazy allocation
-   basic mmap

------------------------------------------------------------------------

# Phase 3: Kernel Memory Management

## 目标

理解 Kernel 自己如何使用内存。

主题：

-   Kernel VA Layout
-   Direct Map
-   vmalloc
-   ioremap
-   Kernel Heap
-   slab/slub

产出：

-   kernel-va-layout.md
-   kernel-heap.md

------------------------------------------------------------------------

# Phase 4: Advanced Process Memory

主题：

-   Anonymous Memory
-   Copy On Write
-   Shared Memory

产出：

-   cow.md
-   shared-memory.md

------------------------------------------------------------------------

# Phase 5: Advanced MM

主题：

-   Page Cache
-   Reclaim
-   LRU
-   Swap
-   OOM

产出：

-   page-cache.md
-   reclaim.md
-   oom.md

------------------------------------------------------------------------

# Phase 6: Optimization & Rust Design

主题：

-   NUMA
-   Huge Page
-   Per CPU allocator
-   Rust Ownership Design
-   Typestate
-   Unsafe Boundary
-   Soundness

最终目标：

设计一个符合 Rust 思维的 Memory Management subsystem。

------------------------------------------------------------------------

# 推荐参考顺序

1.  OSTEP
2.  xv6
3.  Architecture Manual
4.  Linux MM
5.  Asterinas / Theseus
6.  自己的 Rust Design
