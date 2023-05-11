# 1. Arrays: Behind the Scenes 

Since computers don't have an array data type, they allocate a block of memory and then each element is located sequentially within the block. We store the ***base index*** and then compute the address of the nth element. 

```ad-example
icon: file
title: Example Array in Memory
| Location | Value | 
| --- | --- |
| 2000 | F0A3 |
| 2002 | 042B | 
| 2004 | c1F1 |
| 2006 | 0D0B |
| 2008 | 9C2A |
```

The mathematical formula for accessing these individual values is $address_{start} + (index * size)$ and is why C- and C-inspired languages use a zero-index based array system. 

## Indexing on the x64 

The x64 supports direct, indirect, and scaling addressing. Processors create the ***effective address***, or an address programmatically generated for accessing memory,  for a value using the above mentioned formula. In the Intel x64 syntax, it is written as:
$$
[Base + Index \cdot Scale + Displacement]
$$
The terms are defined as below:
- ***Base:*** (register) initial address.
- ***Displacement:*** (constant)"offset". A constant (*immediate*) added to the address.
- ***Index:*** (register/constant) a register added to the address.
- ***Scale:*** (constant) used to multiply the index before adding it to the address.

```ad-info
title: Base vs. Displacement?

The "displacement" is used in Direct Addressing (since we are using a constant, signed integer) and the "base" is used in indirect addressing (since we use a register). 

&ensp;

Both can be used together but this is not covered in this class.
```

This finishes our addressing mode table from earlier.

| Mode | Syntax | Java Equivalent |
| --- | --- | --- |
| Immediate | value | value |
| Register | register | register |
| Direct | label | Memory [label] |
| Direct (Indexed) | [label + reg] | Memory [label + reg] |
| Indirect | [reg] | Memory [reg] |
| Indirect (Indexed) | [reg + reg] | Memory [reg + reg] |
| Indirect (Indexed + Scaled) | [reg + reg * scale] | Memory[reg + reg * scale] |

When doing any of these formats, all four parts of the formula are being used, but "missing" items are filled in. 

```ad-note
title: For Further Examples
For further examples, view Devin Cook's Part 5 Lecture Slide, slides 23-29.
```



# 2. Tables: Organizing Data

Tables can contain any type of data and are accessed using scaling indexing (discussed in  [[#1. Arrays: Behind the Scenes]]). 

```ad-example
icon: file
title: Creating a Table of Long Integers

Creating the table:
~~~asm6502
Years:
	.quad 1776
	.quad 1783
	.quad 1846
	.quad 1850
	.quad 1947
~~~

Accessing the table:
~~~asm6502
mov rsi, 1
mov rcx, [Years + rsi * 8]
~~~
```

```ad-example
icon: file
title: A Table of Strings

Creating the table:
~~~asm6502
Sutter:
	.ascii "John Sutter\0"
Marshal:
	.ascii "James Marshal\0"
Names:
	.quad Sutter
	.quad Marshal
~~~

Accessing the table:
~~~asm6502
mov rsi, 1
mov rdi, [Names + rsi * 8]
```

## Encoding Indexes in Herkey

The following example code will be used for this section:
```asm6502
(1) LDR r4, [42 + r5 * 8]
(2) LDR r4, [r7 + r5 * 8]
```

 **Herkey Direct** (Line 1)
![[Screenshot 2023-04-27 at 4.29.35 PM.png]]

**Herkey Indirect** (Line 2)
![[Screenshot 2023-04-27 at 4.29.44 PM 1.png]]

# 3. Buffer Overflows: Great Responsibility

Operating systems do a good job of projecting programs from being damaged by other programs, but not as good of a job protecting *themselves*. Data is often stored next to the instructions, and it is possible to store too much information, which overflows out of the buffer and overwrites part of the running program. 

It is possible to do this by accident in an assembly program as well, since we have full control. 

```ad-note
title: For Illustration
See Devin Cook's Part 5 Lecture Slide, slides 49-51
```

