# 1. What are Processors?

The Central Processing Unit (***CPU***) is the computer. While there are thousands of versions, each functioning differently (based on the paradigm of form follows function), all of them share the basic building blocks. 

There are two parts to a CPU:
1. Control Logic Unit (CLU)
2. Execution Unit (EU)

## A. CLU

This part controls the processor. It determines when instructions can be executed. It controls internal operations, such as fetching and decoding instructions, while remaining invisible to running programs.

## B. EU 

This part contains the physical hardware that executes tasks. Often modern processors will use many of them in parallel execution.

##### ALU 

The Arithmetic Logic Unit is part of the EU and performs all calculations and comparisons, including special hardware for integer and floating point. 

# 2. Registers

Since assembly does not have the concept of variables, we use registers, or physical locations *on the processor itself*, to store temporary data. Some are accessible to programs and others are hidden. 

##### Why registers? 

Registers are designed to be quickly accessible (due to limitations in accessing memory) for anything the processor needs to keep track of.

## A. General Purpose Registers (GPR)

These registers are designed to be used by programs as needed (often calculations). 

## B. Special Registers

These registers are unaccessible by programs and are instead used by the CLU, such as for control memory usage, program execution thread, etc, etc.

***Instruction Pointer*** (IP or Program Counter): This register keeps track of running program's address (like a line number). 

***Status Register***: This register contains boolean information about the processor's current state.

***Instruction Register*** (IR): This register stores the current instruction being executed.

## C. Register Files

All related registers are grouped into a register file, although to to access and use these files depends on the processor. Sometimes registers are implied or hardwired. 

![[Screenshot 2023-05-15 at 12.18.15 PM.png]]

# 3. Instructions

Assembly does not have the same constructs, e.g., Blocks, If Statements, While Statements, etc etc., as higher level languages, thus we are not abstracted from the architecture of the machine. Since we are on the architecture level, we can only perform series of simple tasks, or ***instructions***. 

These instructions create all the logic needed by a program. The instructions supported by a processor is defined by the ***instruction set***:
- add two values together
- copy a value
- jump to memory location
- etc

# 4. The Intel x64

The x64 is the modern, Intel 64-bit processor platform that has been developed continuously over 40 years.

## A. The OG: x86

The x86 was originally 16-bit when it was released in 1978. It featured 16, 16-bit registers. It was then expanded to 32-bit under the "x86" moniker. For the 64-bit transition, it was renamed "x64".

##### x86 Registers

The original x86 featured 16 registers, 8 of which were open-access and 8 which were hidden, used for memory management. 

- 4 GPR: AX, BX, CX, DX
- 4 Pointer Index: SI, DI, BP, SP
- Restricted 8: CS, DS, ES, FS, GS, SS + IP + Status Register

##### 32-bit Evolution

Old registers obtained the "e" (for extended) suffix for their 32-bit versions. 

###### 64-bit Evolution

Registers obtained the "r" prefix for their 64-bit versions and added 8-additional registers. For hardware consistency, it was possible to get 8-bit values from all registers.

###### 64-bit Register Table

| 64-bit | 32-bit | 16-bit | 8-bit High | 8-bit Low |
| --- | --- | --- | --- | --- |
| rax | eax | ax | ah | al |
| rbx | ebx | bx | bh | bl |
| rcx | ecx | cx | ch | cl |
| rdx | edx | dx | dh | dl |
| rsi | esi | si | | sil |
| rdi | edi | di | | dil |
| rbp | ebp | bp | | bpl |
| rsp | esp | sp | | spl |
| r8 | r8d | r8w | | r8b |
| r9 | r9d | r9w | | r9b |
| r10 | r10d | r10w | | r10b |
| r11 | r11d | r11w | | r11b |
| r12 | r12d | r12w | | r12b |
| r13 | r13d | r13w | | r13b |
| r14 | r14d | r14w | | r14b |
| r15 | r15d | r15w | | r15b |

# 4. Basic Intel x86 Instructions

Each instruction in x86 can have up to 2 operands, which are very versatile in that they can either be a memory address, register, or an immediate value (constant), although certain instructions have limitations on which can be used. 

##### Limitations
- a register must always be involved (both operands cannot access memory at the same time)
- the receiving field cannot be an immediate value

## A. Move Instruction

The Intel Move Instruction combines *transfer, load, and store instructions*. It copies data.

```asm
MOV destination, source

# destination is a register or memory
# source is immediate, register, or memory
```

## B. Add and Subtract

```asm
ADD, target, value

# target is register or memory
# value is immediate, register, or memory

SUB target, value
```
## C. AND and OR

```asm
AND target, value

# target is register or memory
# value is immediate, register, or memory

OR target, value
```

## D. Call 

Tells the processor to start a subroutine (covered in later parts). Returns to current line after call. 

```asm
CALL address

# address is either the address itself or a label
```