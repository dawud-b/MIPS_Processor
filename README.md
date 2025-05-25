# MIPS_Processor
Three different MIPS processors: Single-cycle, 5-stage Software Scheduled, 5-stage Hardware Scheduled.

Each include MIPS assembaly tests, all of which execute properly. 

Supported instructions: add, addi, addiu, addu, and, andi, nor, or, ori, sll, sllv, slt, slti, sra, srl, srlv, srav, sub,
subu, xor, xori, lw, lb, lbu, lh, lhu, lui, sw, beq, bne, j, jal, jr

The Software-scheduled pipeline requires no data hazards by adding nops and reordering insturctions.
The Hardware-scheduled pipeline includes full forwarding, stalling, and flushing to prevent all data hazards and successfully execute any supported instructions in any order.

![image](https://github.com/user-attachments/assets/de06308d-68fe-4d67-93e5-d7f3cf3c073d)
This is the final diagram of the pipeline. It includes five stages: Instruction-Fetch, Instruction-Decode, Execute, Memory, and Write-Back.
Jumps and branches execute in the Decode stage, flushing any instruction in the Fetch stage.

If a data depedency occurs with a consuming instruction in Decode and a producing instruction in Execute (or a load in Memory), then that data will be forwarded next cycle to prevent stalling. If a data hazard cannot be forwarded, a stall will occur. 


