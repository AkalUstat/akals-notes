
# 1. The System Stack: A Pile of Data

A ***Stack*** is a LIFO data structure introduced in CSC 20 and Java. Examples of stacks are:
- Page-visited "back-button" history in a web browser
- Undo sequence in a text editor
- Deck of cards in Windows Solitaire
A processor maintains its own stack in memory which stores integers the size of the bit-size of the system (e.g., a 64-bit system stores 64-bit integers on the stack). The stack allows for ***subroutines***, a simpler version of functions in higher-level languages. The stack is defined in memory by a fixed location pointer (***S0***) locating the bottom and a ***stack pointer*** locating the top.,

There are two approaches to working with the stack:
1. Growing Upwards: S0 is the lowest address in the stack buffer and the stack grows towards higher addresses
2. Growing Downwards: S0 is the highest address in the stack buffer and the stack grows towards lower addresses. 

#### Size of the Stack

As a data structure, stacks can be infinitely deep (unlimited data storage), but since they are implemented using memory buffers on processors (finite in size), if the data exceeds the allocated space, a ***stack overflow*** error occurs error occurs.

# 2. Subroutines: Organizing Your Programs

We cannot have subroutines without the stack since the stack is necessary in saving return addresses for call instructions, backing up and restoring registers, and passing data between subroutines. 

When we call a subroutine:
1. Processor pushes the IP on the stack
2. The IP is then set to the address of the subroutine
3. The subroutine executes and ends with a "return" instruction.
4. The processor pops and restores the original IP
5. Execution continues after the initial call

#### Nesting is Possible: Subroutines Call other Subroutines

Let's look at an example of a subroutine `f()`, which calls `g()`, which furthermore calls `h()`.

What the stack does is it stores the return addresses of the callers (much like the history button in a web browser). As each subroutine completes, the processor pops the top of the stack and returns to the caller. 

![[Screenshot 2023-04-30 at 8.32.01 AM.png]]

## A. x64 Subroutines

```asm6502
CALL address

#address typically is made simpler with a label instead
```

The Call instruction transfers control to a subroutine (may be called JSR on other processors).  The Return instruction marks the end of a subroutine (do not forget - it often will cause your program to run beyond its end!).

```asm6502
RET #no arguments!
```

```ad-example
title: Subroutine Example
![[Screenshot 2023-04-30 at 8.40.40 AM.png]]
```


# 3. Operating Systems: Master Software

An ***operating system*** is a series of programs with special privileges needed by the OS. There are two executing modes for programs on modern processors. 

1. ***Privileged Mode*** (Supervisor Mode): In this mode, programs can run special instructions and talk to all hardware
2. ***User Mode***: In this mode, programs can only execute certain instructions and are limited in their ability to talk to hardware.

## A. Vector Tables

Programs and hardware often need to talk to the OS (e.g., USB port notifying the OS, programs runs an OS function). To accomplish this, the processor can be ***interrupted*** (or alerted) that something must be handled. The processor then runs a special program to handle that event. 

During this interrupt, the device sends the processor a unique ***interrupt number*** that will then be looked up in a ***vector table***, which contains the address of the ***Interrupt Service Routine*** (ISR) to execute for that event. 

![[Screenshot 2023-04-30 at 8.54.54 AM.png]]

When the processor gets an interrupt:
1. Backs up the register file
2. Executes the ISR
3. Upon completion, restores the original executing program and register file

The the ISRs belong to the ***kernel***, or the core of the OS (the vast majority of which is hidden from the user). 


# 3. Interacting with Applications: How We Talk to the OS

Software also needs to talk to the OS, just like hardware ("draw a button", "print a document", etc, etc). There are interrupts specifically designated for software so that a running program can interrupt *itself* with a specific number. 

Programs "talk" to the OS with ***Application Program Interfaces*** (APIs). Application $\rightarrow$ OS $\rightarrow$ IO. This has the benefit of making applications faster and smaller and securing the system by abstracting away the IO from direct access by programs.

The interrupt for programs in assembly is:
```asm6502
SYSCALL
```

#### Subroutines vs. Interrupts

![[Screenshot 2023-04-30 at 9.07.15 AM.png]]

# 4. Linux System Calls

Linux also uses interrupts. Applications don't know where (in memory) to contact the kernel so they ask the processor to do it.

How it works:
1. Fill the registers
2. Interrupt using `syscall`
3. Any results will be stored in the registers

How to call:
1. The `rax` register must contain the syscall number (indicates to the OS what you are trying to do; there are only 329 total calls on a 64-bit UNIX system).
2. Other registers hold data in a rather odd order: `rdi`, `rsi`, `rdx`, `r10`, `r8`

Some calls are listed below:

![[Screenshot 2023-04-30 at 9.14.34 AM.png]]

# 5. Saving Registers and Lost Data

There are limited number of registers and a lot of subroutines need to use (and often modify) registers, so variables we store may be changed. 

There are two solutions to this problem:
1. **Caller saves values**: The caller saves all their register to memory before making a subroutine call and restores them before continuing (not recursion friendly).
2. **Subroutine saves values**: Subroutine pushes registers onto the stack and pops (restores) the old values off the stack before it returns.


![[Screenshot 2023-04-30 at 9.25.23 AM.png]]