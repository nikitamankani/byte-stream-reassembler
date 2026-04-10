# ByteStream Reassembly Engine  
A C-based system for reconstructing byte streams from out-of-order and variable-sized fragments using efficient data structures and memory-safe operations.

---

## Features

**Out-of-Order Reassembly**  
Handles fragments arriving in arbitrary order using offset-based insertion.

**Variable Fragment Support**  
Supports fragments of any size with dynamic memory allocation.

**Sorted Merge Structure**  
Maintains a sorted linked list of fragments and performs merge-on-insert to build contiguous data blocks.

**Overlap Detection**  
Rejects fragments that overlap existing data to ensure correctness and data integrity.

**Completion Detection**  
Identifies when a full byte stream has been successfully reconstructed.

**Resource Constraints**  
Limits maximum packet size and number of active packets to prevent excessive memory usage.

**Timeout Cleanup**  
Removes stale/incomplete packets using a pruning mechanism.

**Memory Safety**  
Uses malloc, realloc, and free carefully to ensure no memory leaks.

---

## Tech Stack

| Component | Technology |
|----------|-----------|
| Language | C |
| Concepts | Data Structures, Memory Management, Systems Programming |

---

## 📁 Project Structure

```
ByteStream-Reassembly/
├── defrag.h     # structure definitions and function declarations
├── defrag.c     # core reassembly logic
├── main.c       # test driver and simulation
└── README.md
```
--- 

## Core Design

### System-Level Structure
- Maintains a linked list of active packet assemblers  
- Allows dynamic handling of multiple concurrent streams  

### Packet-Level Structure
- Each packet uses a sorted linked list of fragments  
- Enables efficient insertion, merging, and validation  

---

## Core Algorithm

### Fragment Insertion (O(n))

1. Validate bounds (offset + length within expected size)  
2. Find correct insertion point in sorted list  
3. Check for overlap with neighboring fragments  
4. Insert fragment into list  
5. Merge adjacent fragments if contiguous  

---

## Completion Criteria

A packet is considered complete when:

- Last fragment has been received  
- Total bytes received matches expected size  
- Fragment list reduces to a single node  
- Final fragment starts at offset 0  

---

## How to Compile & Run

### Compile

```bash
gcc main.c defrag.c -o reassembler
