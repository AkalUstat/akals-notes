# 1. Compilers, Assemblers, and Linkers

When you hit "compile" or "run" many things happen in the background. 

***The Development Process***: 
1. Write program in high-level language
2. Compile program into assembly
3. Assemble program into objects
4. Link multiple objects programs into one executable
5. Load executable into memory
6. Execute it

## A. Your Code to Binary

At the base level, when we are editing code in a Code Editor, where we get type-checking and other features, that functionality is provided by an ***Interpreter***, which never compiles the code, but run parts of their own program.

A ***compiler*** converts programs from high-level languages into assembly language.

From this compiled program, an ***assembler*** converts assembly into binary readable by the processor. This results in an ***object file***, which is not executable at this point. It contains instructions and information on how to link into other executable "units".

Often, since parts of a program are created separately (executable "units" or *objects*). A ***linker*** joins them into a single file. It connects labels from the object that defines it to the one that uses it. (One object can call another). 

The Unix headers *crt1.o* and *crti.o* (automatically supplied) reference a subroutine called `_start`, provided by your own program.

# 2. Assembly Basics

Assembly programs allow you to write machine language programs in easy-to-read text. Assembly varies based on specific processor architecture (does not "cross-port").

***Assembly Benefits***:
1. Consistent way of writing instructions
2. Automatically count bytes and allocates buffers
3. Labels are used to keep track of addresses

### I. Consistent Instructions

Assembly combines related machine instructions into a single notation (and name) called a ***mnemonic***.

### II. Count and Allocate Buffers

Assembly automatically counts bytes and allocates buffers (since miscounts done by hand are common). 

### III. Labels and Addresses

Addresses are stored using labels (nice, easy to use names for addresses). 

## A. Syntaxes

### I. AT&T Syntax
- Unix and Linux dominance
- registers prefixed by '%' and values with '$'
- receiving register is *last*

### II. Intel Syntax
- Created by MS
- dominant on DOS/Windows
- neither registers or values have a prefix
- receiving register is first

# 3. Assembly Program Structure

There are two parts to an assembly program, the *data* and *text* section.

***Data Section***: allocates bytes to store constants, variables, etc 

***Text Section***: contains the instructions that will make up the program.

## A. The Data Section

### I. Directives

A directive is a special command for the assembler. It starts with a "."

They can:
- allocate space
- define constants
- start the text/data section
- make labels "global" for the linker

### II. Labels

Labels are defined by an identifier followed by a colon. When an assembler sees a label declaration, it saves the current address into a table of labels stored in the ***object file***. **Labels are addresses**. Labels also do not generate any bytes in the final machine code.

# 4. Unix Basics

Unix was developed at AT&T's Bell Labs in 1969 and was designed for mainframes and to be stable/powerful. 

## A. Command Line Interfaces

Since Unix was developed before GUIs, all interaction with the computer was done through command line interfaces (CLIs). This interface is text only but performs the same commands as GUIs.

Each command starts with a name followed by arguments which are separated by spaces. 

```
name argument1 argument2
```
***Some UNIX Commands***:
- `ls`: List all files in CWD
- `ll`: List Long. Shortcut for `ls -l`
- `pwd`: Print Working Directory. Prints out your current path.
- `cd`: Change Directory.
- `mkdir`: Make Directory.
- `rm`: Remove. Deletes a file. There is no way to recover this file.
- `nano`: a UNIX text editor. 
- `as`: GNU assembler. Converts an assembly program into an object. It will alert you of any syntax errors or unrecognized mnemonics (typos). The command is written as follows:
```shell
as -o lab.o lab.asm
```
The -o specifies that the next name listed is the output file. The third argument is the input file.
- `ld`: GNU linker. Takes 1+ objects and links them into an executable. Any unresolved labels will be brought to your attention. The command is written as follows:
```shell
ld -o a.out csc35.2 lab.o
```
# 5. Machine Language

Eventually, your programs are broken down into their raw binary form, called ***Machine Language*** or Machine Code.

Each instruction in your program is ***encoded*** into a compact binary format. It is easier for the processor to interpret and execute this encoding. However, not all encodings are equal: some instructions require more bytes than others. 

Each instruction must contain everything the processor needs to know to do something (like functions in java: they need a name and arguments). Thus, each instruction has a unique ***Operation Code (Opcode)*** that specifies the exact operation to be performed by the processor. In assembly, we use friendly names for these called mnemonics. The opcode is followed by various operands (data to be used in the operation). 

# A. Encoding

Since x64 encoding is complex, we will use a fictitious processor called the Herky 6000 Processor, which mirrors the Intel behavior but is easier to encode. Its specifications are:
- each instruction is 24-bit (3 byte)
- 16 GPR (using Intel names)
- supports all major addressing modes
- most instruction fields line up cleanly on each nibble $\rightarrow$ each hex digit is a field

![[Screenshot 2023-05-15 at 3.59.13 PM.png]]

![[Screenshot 2023-05-15 at 4.00.19 PM.png]]

Since instructions oft need to store an immediate, the Herky Processor allows the second operand to store the byte count ($2^n$, where $n = 0,1,2,3,4$).