
# 1. von Neumann Architecture

Modern computers are based on the design of John von Neumann, who simplified the construction and use of computers.

There are three main attributes to this architecture:
1. Programs are stored and executed in memory
2. Separation of processing from memory
3. Different system components communicate oven a shared bus

## A. The Bus

The bus is an electronic pathway that transports data between components (kinda like a highway, data moves on shared paths). There are three categories/sets of signals on the memory bus:
1. address bus
2. data bus
3. control bus

#### Address Bus

This bus is used by the processor to access a specific piece of data. This "address can be":
- a specific byte in memory
- a unique IO port
- etc
The more bits it has, the more memory can be accessed.

![[Screenshot 2023-04-30 at 9.43.33 AM.png]]

#### Data Bus

The actual data travels over the data bus. The number of bits that the processor uses (as its natural unit of data) is called a ***word***. A system is typically defined by its word size. For example:
- 8-bit system uses 8-bit words
- 16-bit system uses 16 bits (2 bytes) words
- 32-bit system uses 32 bits (4 bytes) words

#### Control Bus

The control bus controls the timing and synchronizes the subsystems. It Specifies what is happening, e.g., read data, write data, reset, etc, etc. 

![[Screenshot 2023-04-30 at 9.45.44 AM.png]]

## B. von Neumann Architecture Today

Most modern systems use a modified version of his design. In particular, they have a special high-speed bus between the processor/memory (like an HOV lane or high-speed rail; fixed source and destination and goes faster than the freeway). 