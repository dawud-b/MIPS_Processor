# MIPS_Processor
Three different MIPS processors: Single-cycle, 5-stage Software Scheduled, 5-stage Hardware Scheduled.

Each include MIPS assembaly tests, all of which execute properly. 

Supported instructions: add, addi, addiu, addu, and, andi, nor, or, ori, sll, sllv, slt, slti, sra, srl, srlv, srav, sub,
subu, xor, xori, lw, lb, lbu, lh, lhu, lui, sw, beq, bne, j, jal, jr

The Software-scheduled pipeline requires no data hazards by adding nops and reordering insturctions.
The Hardware-scheduled pipeline includes full forwarding, stalling, and flushing to prevent all data hazards and successfully execute any supported instructions in any order.

