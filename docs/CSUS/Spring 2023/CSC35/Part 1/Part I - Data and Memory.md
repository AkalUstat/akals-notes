## 1. Binary Numbers

The binary number system is base 2 and features only two digits: 0 and 1. 

To write a number in binary (from decimal), we use the following table:

| $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
| -- | -- | -- | -- | -- | -- | -- | -- |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 
| - | - | - | - | - | - | - | - 

 ***Bit***: one binary digit. 1 or 0. shorthand is "b".
 
 ***Byte***: a group of 8 bits. shorthand is "B".

 ***Nibble***: half of a byte or 4 bits. 

### Hexadecimal Numbers

Since binary numbers are cumbersome and error prone to write, especially with higher numbers of digits, computer scientists have come up with the *hexadecimal* system to store binary information. Since the hexadecimal system is base 16, one hexadecimal digit is equivalent to 4 bits. ($2^4 = 16$)

| Hex | Decimal | Binary | |  Hex | Decimal | Binary |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | 0 | 0000 | | 8 | 8 | 1000
| 1 |1 | 0001 | | 9 | 9 | 1001
| 2 | 2 | 0010 | | A | 10 | 1010
| 3 | 3 | 0011 | | B | 11 | 1011
| 4 | 4 | 0100 | | C | 12 | 1100
| 5 | 5 | 0101 | | D | 13 | 1101
| 6 | 6 | 0110 | | E | 14 | 1110
| 7 | 7 | 0111 | | F | 15 | 1111


## 2. How Text is Stored

Since computers need to often store and transmit text data, it stores individual symbols as "characters", or rather the integer representation of each character. This integer representation is based on the "standard" being used, e.g., ASCII (7 bits) or UTF-8 (21 bits).

### Ascii Tips and Tricks

Each character has a unique value in the ASCII system, but it has its interesting quirks. For example, for alphabetic characters, upper and lowercase values are only 32 points apart. This means that to convert an uppercase letter to a lowercase letter, simple add 32 to its code - or rather $2^5$, so this means just change the $2^5$ place in the binary representation. 

To change number characters between the character code itself and the binary representation:
- Character $\rightarrow$ Binary: Clear the upper nibble (set it to 0000)
- Binary $\rightarrow$ Character: Set the upper nibble to 0011

# 3. Computer Memory

Memory is basically an array. That's it. That's all. It's also referred to as storage and it stores both running programs and their related data together. 

![[Screenshot 2023-05-15 at 11.47.16 AM.png]]

Memory is divided into storage locations that each hold 1 byte (8 bits). Each of these can be accessed using a unique identifier referred to as an *address* (basically the array index). 
