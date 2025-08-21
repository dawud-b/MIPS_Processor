# MIPS Processor Project  

This project implements three versions of a MIPS processor, designed to highlight different approaches to instruction execution and hazard handling:  

- **Single-Cycle Processor**  
- **5-Stage Software-Scheduled Pipeline**  
- **5-Stage Hardware-Scheduled Pipeline**  

Each processor includes MIPS assembly test programs, all of which execute correctly.  


## Overview  

- Designed mainly with structural VHDL with some dataflow
- Implements a subset of the MIPS32 ISA  
- Supports arithmetic, logical, shift, memory, and control flow instructions  
- Demonstrates trade-offs between software hazard scheduling and hardware hazard detection 
- Includes fully functional hazard detection and forwarding logic in the hardware-scheduled pipeline  
- Performance of each CPU design was analyzed and compared  


## Supported Instructions  

### Arithmetic & Logical  
`add, addi, addiu, addu, sub, subu, and, andi, or, ori, xor, xori, nor, slt, slti`  

### Shift  
`sll, sllv, sra, srav, srl, srlv`  

### Memory Access  
`lw, lb, lbu, lh, lhu, sw, lui`  

### Control Flow  
`beq, bne, j, jal, jr`  



## Processor Implementations  

### Single-Cycle Processor  
- Executes one instruction per clock cycle  
- Simplest implementation — no pipelining  
- Limited performance, but easy to verify correctness  

### Software-Scheduled Pipeline (5-stage)  
- Includes 5-stage pipeline: IF, ID, EX, MEM, WB
- Requires the programmer/compiler to insert `nop`s and reorder instructions to avoid hazards  
- No runtime hazard detection — only safe instruction sequences execute correctly  

### Hardware-Scheduled Pipeline (5-stage)  
- Fully pipelined with:  
  - Forwarding (EX/MEM → ID/EX paths)  
  - Stalling (for load-use hazards)  
  - Flushing (for control hazards)  
- Executes supported instructions correctly in any order  
- Provides a more realistic model of modern pipelined CPU designs  

## Pipeline Diagram


![Pipeline Diagram](https://github.com/user-attachments/assets/de06308d-68fe-4d67-93e5-d7f3cf3c073d)
_*Diagram for Hardware-Scheduled Pipeline_

The 5-stage pipeline includes:  

1. **Instruction Fetch (IF)**  
2. **Instruction Decode (ID)**  
3. **Execute (EX)**  
4. **Memory Access (MEM)**  
5. **Write Back (WB)**  

- Jumps and branches are resolved in the Decode stage, flushing any instruction in Fetch  
- Forwarding resolves most data hazards by bypassing results to dependent instructions  
- Stalling occurs only when hazards cannot be resolved through forwarding (e.g., load-use)  

## Testing  

The design was tested using a tool flow based on Quartus and MARS (MIPS Assembler and Runtime Simulator).  

- Each register or memory write was compared against MARS outputs for correctness  
- All assembly programs in the `/mips/` directories were tested and passed successfully  
- Individual components were verified with dedicated testbenches, located in each processor’s `/test/` directories  
- Testbenches were simulated using QuestaSim to ensure correct functionality before integration into the top-level design
- Benchmarks included in Processor_Performance.pdf

## Key Takeaways

- **Single-Cycle Processor:**  
  - Simplest design but longest execution times due to long cycle period.  
  - Performs well in terms of CPI (always 1.0).  

- **Software-Scheduled Pipeline:**  
  - Faster cycle period due to pipelining.  
  - Performance suffers on hazard-heavy applications, like Grendel, due to many inserted NOPs.  
  - Can outperform hardware-scheduled pipeline in specific workloads (shown with BubbleSort) thanks to instruction reordering.  

- **Hardware-Scheduled Pipeline:**  
  - Best overall design, balancing forwarding, stalling, and flushing.  
  - Outperforms single-cycle on all workloads.  
  - Usually faster than software-scheduled, except in cases where reordering benefits the latter.  





