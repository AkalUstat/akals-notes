Stacks and Queues

# I. Abstract Data Types

Data types specify two things
1. They set the possible, valid values
2. Operations (methods/functions) on the data and errors that may occur

While the core data types of a language are called *primitive data types*, which are building blocks for other more complex data types (e.g., int, char, double, etc),, *abstract data types* implement data types internally (hide them) and only allows the client to interact with specified operations and properties, called an *interface*. This abstracts implementation from behavior, so that even if the entire underlying data type is replaced, the ADT is not broken.

# II. Stacks
Piles of data

Stacks are FILO or LIFO ADTs - like a stack of dishes. Data is added/removed from the "top";  head of the stack when implemented using a linked list.
![[Screenshot 2023-10-03 at 8.45.12 PM.png]]
###### Errors
Stacks mainly throw errors when pop() and top() are called on an empty stack

###### Implementation
Don't implement using dynamically sized array, because pop/push would become O(n) because it requires an array resize. 
An optimization (still not a good one) is to resize every n elements and increase capacity by n elements, but you would need to keep an end index.
Fixed size arrays work if  you either throw an Overflow Error or discard the bottom of the stack if it is filled.
![[Screenshot 2023-10-03 at 8.42.18 PM.png]]

# III. Queues
Queue ADT is like a line: FIFO, LILO. Add to end of queue (Tail), remove from the front (head). 

![[Screenshot 2023-10-03 at 8.45.27 PM.png]]![[Screenshot 2023-10-03 at 8.46.06 PM.png]]o

# IV. Deque
A variant of the queue: ***d***ouble-***e***nded ***que***ue. Allows removal and insertions from both ends, as it is the union of a Stack and Queue.
![[Screenshot 2023-10-03 at 8.47.19 PM.png]]

#### Advantages
It functions as either. The add front operation is "redo" or "undo" for a queue removal. 
Deques requires a double-linked list (b/ then the tail remove would be O(n)). So, auxilary space usage is O($n^2$). 
![[Screenshot 2023-10-03 at 8.49.12 PM.png]]

# V. Evaluating Expressions

## A. Math Notations

#### Infix Notation
Not friendly to stack or queue, but plenty human friendly.
$$ a + b / c \cdot d $$ 
#### Prefix Notation
AKA *Polish Notation*: put operator before the operands:
$$ + a b$$ or $$ \space / a \space b $$
#### Postfix Notation
*Reverse Polish Notation*: put operator at the end. Since it is last, we can use it as a trigger to execute math. No need for parensthesis. 

###### Computing Postfix
Need a: queue for the values and operators, and a stack.
Steps:
1. While input
	1. dequeue a token
			1. if value, push it to stack
			2. if operator, 
				1. pop two numbers from the stack
				2. compute result
				3. push it to stack
			
	   1. end if
 1. end while

###### Infix to Postfix/Prefix Conversion
1. Make a Fully Paren Expr (FPE). One pair encloses each operator and its operands.
2. move operators to either start or end of each sub expression

#### Infix to Postfix Algo
***Shunting yard algo***: Dijkstra. Most basic version requires FPE.
###### FPE Version
1. While queue has tokens
	1. read a token from the input queue
	2. if token is
		1. operand: add it to operator queue
		2. operator: push it to stack
		3. "(": push it to stack
		4. ")":
			1. while top of stack isn't a "("
				1. pop an operator
				2. add it to the output queue
			2. end while
		5. pop and discard extra "(" at the end
	3. end if
2. end while 
###### Non FPE Version
Just change operator rules in step 1.2:

if operator is left-associative: 
1. while tope of stack is >= operator and not a "(":
	1. pop stack
	2. add it output queue
2. end while
If operator is right associative:
1. while top of stack is > operator and not a "("
	1. pop stack
	2. add to output queue
2. end while
push operator to stack. 
$+ \space - \space \cdot \space / \space$ are left associative. exponent is right associative.

