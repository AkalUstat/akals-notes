# 1. x86 Jump Instructions: Mario Time

Since assembly does not provide high-level expressions or blocks, we have to jump over code to implement this logic. The processor achieves this by moving the ***Instruction Pointer*** (discussed in Part 2) to a new address and continuing execution. 

There are many types of jumps.

## Unconditional Jumps

This is a simple transferring of a program to a new address (a la `goto`).

```asm6502
JMP address
```

![[Screenshot 2023-04-27 at 4.42.29 PM.png]]

## Conditional Jumps

Conditional jumps will, as the name suggests, only jump if a certain condition is met. This is used to implement branching logic. In order to do this, we first must use a comparison statement to determine if we can or will jump.

```asm6502
CMP arg1, arg2

# arg1 = register or memory
# arg2 = immediate, register, or memory
```
![[Screenshot 2023-04-27 at 4.44.51 PM.png]]![[Screenshot 2023-04-27 at 4.45.17 PM.png]]

There are many conditional jump statements for readability. 

| Jump | Description |
| --- | --- |
| `je` | Jump Equal |
| `jne` | Jump Not Equal |
| `jg` | Jump Greater than |
| `jge` | Jump Greater than or Equal |
| `jl` | Jump Less than |
| `jle` | Jump Less than or Equal |

![[Screenshot 2023-04-27 at 4.47.55 PM.png]]

# 2. If Statements on the x86

To make this simpler (and use less LOC), in assembly, we will reverse the logic of the `if` statement. If we pass the test condition, we will continue to execute downwards as normal. If it is false, then and only then will we jump over the code.

```ad-note
title: For Illustration
See Devin Cook's Part 6 Lecture Slide, slide 26-28.
```

## Throw a Wrench in the Works With an Else Clause

We do similar logic as the plain `if` statement, except for the `false` case will jump to its own block, and we jump over the `false` block at the end of the `true` block (otherwise, assembly just executes instructions as they come and the '`false` block will be executed as well').

# 3. Loops

## While Loops
We write `while` loops in assembly basically like `if` statements. To create a while statement:
1. Start with an If statement
2. Add an unconditional jump at the end of the block that jumps to the beginning
The initial if statement will break the loop.

```asm6502j
While:
	cmp rdi, 21
	jge End

	#true block
	jmp While
```

## Do While Loops

A `while` loop implementation, but with a post test (will run at least once).
```asm6502
Do:
	#true block

	cmp rdi, 21
	jl Do
```

In this case, it actually costs us less LOC do use positive (straightforward logic) as compared to negative logic.

# 4. Best Friends: Addressing and Loops

In `for-each` loops in high level languages, we can use the index as a variable to access each element in an array. In assembly, we accomplish this by using a register to store the index. For example:
```asm6502
.intel_syntax noprefix
.data
Greeting: 
	.ascii "Hello"

.text
.global _start:
_start:

	mov rdi, 0

Loop:
	cmp rdi, 4
	jg End # end loop

	movb [Greet + rdi], 33
	add rdi, 1
	jmp Loop
 End:
	 call Exit
```

# 5. Switch Statements on x86: The Why for C, Java, and C#

The Switch behavior for C, Java, and C# is strange/peculiar in that they require break statements for each case of the switch, otherwise the execution falls through each of them. This is because for efficient and cast compilation to ASM, the ASM behavior is mapped almost one-to-one. For example:
```asm6502
mov rdi, 13
cmp rdi, 10 # equivalent of "case 10:" in C
je case_10 # jump to handler

cmp rdi, 11 # equivalent of "case 11:" in C
je case_11 # jump to handler

jmp default # default case

case_10: # each of these "falls through" because we don't jump
	call Handler10
case_11:
	call Handler11
default:
	call Default
```

So, in C, Java, and C#, a `break` statement just maps to a jump statement. Thus, our handlers, with `break`s this time, would be written as:
```asm6502
case_10: # now these cases are one-and-done
	call Handler10
	jmp End
case_11:
	call Handler11
	jmp End
default:
	call Default
	jmp End
End:
	call Exit
```

