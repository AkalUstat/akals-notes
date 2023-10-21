# 1. Buffers

A ***buffer*** is any allocated block of memory that contains data (e.g., text, image, file, etc). There are several assembly ***directives*** which allocate space, a few of which we have covered: 

| Directive | Purpose | 
| --- | --- |
| `.ascii` | Allocate enough space to store an ASCII string. |
| `.quad` | Allocate 8-byte blocks with initial value(s). | 
| `.byte` | Allocate byte(s) with initial values.
| `.space` | Allocate any size of empty bytes (with initial values). | 

# 2. Addressing Modes

Processors often need to access memory to read values and store results. We've done the basics of reading and storing single values using registers so far, but we need to do more complex things such as:
- access items in an array
- follow pointers
- etc

How the processor can go about reading and writing that data is called an addressing mode. There are 4 basic modes:
- Immediate Addressing
- Register Addressing
- Direct Addressing
- Indirect Addressing

## I. Immediate Addressing

An immediate is a constant value often stored as part of an instruction. Thus, it is immediately available. 

## II. Register Addressing

Register addressing is used in almost all computer instructions, where a value is read from or stored into one of the registers. 


![[Screenshot 2023-05-15 at 4.11.43 PM.png]]

## III. Relative Addressing

We can also use relative addressing by adding a value to the IP/Program Counter. This means that the instruction can just store the difference from the current instruction address (takes less storage than a full 64-bit address). This allows a program to be stored anywhere in memory and still work.

This way of storing addresses is often used in jump statements and to access local data (load/store).

## IV. Direct Addressing

In direct addressing, the processor reads data directly from an address. This commonly used to get a value from a "variable" or read items in an array.

## V. Register Indirect Addressing

Register indirect reads data from an address stored in a register (like ***pointers***). It's just as fast as direct addressing and with the benefit that the processor already has the address. Register indirect requires square brackets. 

# 3. Sizing Instructions

Intel can load/store 1-, 2-, 4-, or 8- byte values. The assembler differentiates between them by looking at the size of the register. However, sometimes, the number of bytes can't be determined (such as loading from or writing into memory). In this case, it will report as an error since it cannot properly encode the instruction.

To deal with the "ambiguous operand size error", the GAS assembler allows us to place a single character after the mnemonic to tell it how many bytes will be processed during the operation. 

| Suffix | Name | Size | 
| --- | --- | --- |
| `b` | byte | 1 byte |
| `s` | short | 2 bytes |
| `l` | long | 4 bytes | 
| `q` | quad | 8 bytes |

# 4. Endianess

On a 64-bit system, the word, or the byte-size of each basic piece of data, is 8 bytes. So, when we store something, we need to use all 8 bytes. But in what order do we store them?

In the ***Big Endian*** approach, we store the Most Significant Byte (MSB) first. In the ***Little Endian*** approach, we store the Least Significant Byte (LSB) first.

This is important since if two systems (the system that wrote the data and the one that reads the data) use different formats, the data will be interpreted incorrectly (as hopelessly mangled junk most of the time). So, we cannot assume that data accessed from secondary storage or any file format will match the processor's format.