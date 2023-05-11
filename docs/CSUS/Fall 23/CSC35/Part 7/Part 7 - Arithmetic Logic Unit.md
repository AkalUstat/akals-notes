Math!

# 1. Adding Binary Numbers

Computers add binary numbers the same way that we add numbers in decimal format. They align columns, add, and carry over "1"s to the next column. This operation is completed by a processor component called the ***adder***. 

## Negative Binary Numbers? 

In the decimal system, we prefix negative numbers with a minus sign. However, computers can only store "1"s and "0"s, so we need some other way to store this marking. 

#### A. Signed Magnitude

In this system, we use the ***most significant byte*** (MSB) to store this identification. "0" in the MSB indicates a positive number and "1" a negative number. Since this is identical to an unsigned number without context, it is up to the developer to indicated whether a number is signed or unsigned. 

The range of an 8-bit signed magnitude number is from -127 to 127.

```ad-example
title: 8-bit 13 & -13 in Signed Magnitude

13:
<table>
	<tr>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>1</td>
		<td>1</td>
		<td>0</td>
		<td>1</td>
	</tr>
</table>

&ensp;

-13:
<table>
	<tr>
		<td>1</td>
		<td>0</td>
		<td>0</td>
		<td>0</td>
		<td>1</td>
		<td>1</td>
		<td>0</td>
		<td>1</td>
	</tr>
</table>
```

###### Disadvantages of Signed Magnitude

Signed magnitude accomplishes one goal, but introduces other problems. For one, it requires the system to check the sign bits each time (e.g., add if both are positive, subtract if one is negative, etc, etc). It also introduces *positive* and *negative* zero. 


#### B. 1s Compliment

1s compliment is built on top of the same idea as Signed Magnitude, i.e., "0" denotes a positive number and "1" a negative number. However, 1s Compliment accomplishes this by inverting each bit (0 $\rightarrow$ 1 and 1 $\rightarrow$ 0) to create the compliment of the original number. Logically, this is equivalent to subtracting the original number from 0. 

An 8-bit 1s Compliment number can range from -127 to 127.

```ad-example
title: 8-bit 13 and -13 in 1s Compliment

13: 
<table>
<tr>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>1</td>
</tr>
</table>

&emsp; 

-13:
<table>
<tr>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>0</td>
	<td>1</td>
	<td>0</td>
</tr>
</table>
```

###### Advantages

This results in very simple rules for adding & subtracting. Just simply add the numbers. 5 -3 is the same as 5 + (-3).

###### Disadvantages

1s Compliment still results in positive and negative zero. 

#### C. 2s Compliment

2s Compliment is the final form of all of these strategies and is used by practically all modern computers. A 2s Compliment is created by inverting each bit and then adding +1 (same steps in either direction). This is logically equivalent to subtracting the number from $2^n$, where $n$ is the total number of bits in the integer. 

```ad-example
title: 8-bit 13 and -13 in 2s Compliment

13: 
<table>
<tr>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>1</td>
</tr>
</table>

&emsp; 

-13:
<table>
<tr>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>0</td>
	<td>1</td>
	<td>1</td>
</tr>
</table>
```

The instruction for 2s Compliment negation on x86 is:
```asm6502
NEG register
```

###### Advantages

Once again, numbers can simply be added. In this addition, the extra carry "1" that may be left over at the end can be thrown away. This is great for hardware since the processor only needs to know how to add.

Additionally, there is only one zero in this format and the range supports an additional integer (e.g. an 8-bit integer can range from -128 to 127).

```ad-caution
title: Processors are dumb

Processors don't know and don't care whether a number is signed or unsigned; things will work either way. So, it is up to you to keep track (since instructions often vary depending on what kind of integer you are expecting)!
```

## Addition and Subtraction on the x86

Both addition and subtraction take two operands and store the result in the first operand. The instructions for both are listed below:

```asm6502
ADD target, value
# target is register or memory
# value is immediate, register, or memory
```

```asm6502
SUB target, value
# target is register or memory
# value is immediate, register, or memory
```

# 2. Multiplication

The processor really only knows how to add. Historically, processors have done multiplication using successive additions, e.g., $4 \cdot 5$ would add $5$ together 4-times. This is an inefficient algorithm (not $O(1)$). So, nowadays computers do long multiplication just as we do in the decimal system. This fixes the number of addition to 8, 16, 32, or 64 depending on the size of the integers.

```ad-example
title: Unsigned, 4-bit addition. 13 * 10

![[Screenshot 2023-04-29 at 11.47.55 AM.png]]

```

```ad-note
title: Muliplication Bit Count

The size of the product is 2x the original, e.g., 2 4-bit numbers multiplied will result in one 8-bit product.
```

## Multiplication on the x86

The unsigned instruction for multiplication on the x86 is:
```asm6502
MUL operand

# operand must be register or memory
```

and signed multiplication is:
```asm6502
IMUL operand

# operand must be register or memory
```

The first operand must be stored in `RAX` and the second operand must be provided from register or memory only. 

This operand, as discussed previously, has a product with double the bit size of its inputs. How do we store this result? It is often too large to fit into a single register. 

![[Screenshot 2023-04-29 at 11.57.32 AM.png]]
Multiplication on the x86 uses two registers: `RAX` for the lower 8 bytes and `RDX` for the upper 8 bytes in order to maintain precision. 

```ad-warning
Multiplication overwrites any data already existing in `RAX` or `RDX`, so it that data is important, BACK IT UP.
```

There are additionally "short" IMUL instructions that store the multiplication product of unsigned integers in one register, but that is beyond the scope of this course. 

# 3. Extending Byte Size

We often find the need to extend, or move, data from smaller byte sizes to greater bit size, e.g. 8-bit to 16-bit. 

For unsigned numbers, this is easy. Just add more zeros on the left side, as we do with normal decimal numbers.

For signed numbers, this doesn't work because simply adding zeroes will change a negative number to a positive number. 

#### A. Extending Signed Magnitude

1. Copy the old sign-bit (MSB) to the new sign-bit (new MSB)
2. Fill the in-between with zeroes (and overwrite the old sign bit with one too)

```ad-example
title: Extending -77
Old:
<table>
<tr>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>0</td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>1</td>
</tr>
</table>

Extended:
<table>
<tr>
	<td>1</td>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td>0</td>
	<td></td>
	<td>0</td>
	<td>1</td>
	<td>0</td>
	<td>0</td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>1</td>
</tr>
</table>
```

#### B. Extending 2s Compliment

Only one rule: copy the old MSB to all the new bits.
```ad-example
title: Extending -77 in 2s Compliment
Old:
<table>
<tr>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>0</td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>1</td>
</tr>
</table>

Extended:
<table>
<tr>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td>1</td>
	<td></td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>0</td>
	<td>1</td>
	<td>1</td>
	<td>0</td>
	<td>1</td>
</tr>
</table>
```

# 4. Division

Division is similar to multiplication. Division stores the input ***numerator*** in `RAX` (lower 8 bytes) and `RDX` (upper 8 bytes). The output is stored with the ***quotient*** (whole number) in `RAX` and the ***remainder*** in `RDX`.

Unsigned:
```asm6502
DIV denominator

# denominator is register or memory ONLY
```

Signed:
```asm6502
IDIV denominator

# denominator is register or memory ONLY
```

![[Screenshot 2023-04-29 at 12.17.33 PM.png]]

#### Division Rules
1. The numerator *must* be sign-expanded to the destination size (2x the original), since division halves the number of bytes. This must be done before hand.
2. We must setup RDX before division. For unsigned numbers, input 0. For signed numbers, RAX must be sign expanded into RDX. There are special instructions for this listed below:

```asm6502
# 16 bit: Extends AX → into DX
CWD # Convert Word Double

# 32 bit: Extends EAX → into EDX
CDQ # Convert Double Quad

# 64 bit: Extend RAX → into RDX
CQO #Convert Quad Oct
```

```ad-example
title: 64-bit division -1846 by 42
~~~asm6502
MOV rax, -1846 #RAX is the dividend
MOV rbx, 42 #Divisor
CQO #Sign Extend dividend in RAX into RDX
IDIV rbx #RAX gets the quotient and RDX the remainder
~~~
```


# 5. Comparison

It's basically just subtraction! The second argument is subtracted from the first. 
- A - B = a positive number ? A was larger
- A - B = a negative number ? B was larger
- A - B = 0 ? Both are equal

The result itself is thrown away. 

```asm6502
CMP arg1, arg2
#arg1 is register or memory
#arg2 is immediate, register, memory
```

Ok, so if the result is thrown away, then what do we use after the comparison? We use ***flags***, or boolean values stored as individual bits in the ***Status Register*** that indicate the result of the action.

#### Types of Flags

1. ***Zero Flag*** (ZF): True if the last comparison resulted in zero (indicates equality)
2. ***Sign Flag*** (SF): True if the MSB of the result is 1 (indicates a negative 2s Compliment number). Meaningless of the operands are interpreted as unsigned.
3. ***Carry Flag***: (CF): True if a 1 is "borrowed" in subtraction or "carried" in addition. In unsigned numbers this indicates overflow (too big) in addition or underflow (too small) in subtraction. 
4. ***Overflow Flag*** (OF): aka "Signed Carry Flag". True if the sign bit changed when it shouldn't have. Indicates overflow or underflow. 

#### Flags in Context of Jump Instructions

Equality:

| Jump | Description | When True |
| --- | --- | --- |
| JE | Equal | ZF = 1 |
| JNE | Not Equal | ZF = 0 |

Signed Jump:

| Jump | Description | When True |
| --- | --- | --- |
| JG | Jump Greater than | SF = OF, ZF = 0 |
| JGE | Jump Greater than or Equal | SF = OF |
| JL | Jump Less than | SF != OF, ZF = 0 |
| JLE | Jump Less than or Equal | SF != 0 |

Unsigned Jump:

| Jump | Description | When True |
| --- | --- | --- |
| JA | Jump Above | CF = 0, ZF = 0 |
| JAE | Jump Above or Equal | CF = 0 |
| JB | Jump Below | CF = 1, ZF = 0 |
| JBE | Jump Below or Equal | CF = 0 |

