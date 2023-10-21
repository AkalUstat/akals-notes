Linked Lists

# I. Data Structures
*Data structures* are techniques of storing and organizing data (the how). Two big examples are arrays and linked lists. The efficacy of each depends on needs: how data is accessed. 

## A. Arrays
Arrays are a fundamental way of storing data. They are continuous blocks of memory of the same time. Continuity mean that random access is O(1). The access formula is:
$$ start + (index * element_size) $$ This calculation also makes the auxiliary storage overhead O(1) as well. 

#### Resizing Arrays
Since arrays require all elements to be stored continuously, increasing the size of the array means that we must copy all data from the old block into a new one. This is an O(n) operation.

#### Fixed Size Arrays
The fixed size of an array is its *capacity*. We keep it partially filled, keeping an *end* index for the last added item. 

If we maintain a *start* and *end* index, we can create ***fixed-size wrapping arrays***, which wrap around to index 0, replacing data at the start, once we reach the end of the array. This is useful if old data can be discarded or if the 1rst or last items can be removed. 

## B. Linked List 
A linked list is a chain of values. A ***node*** in the list, by definition, contains a value, and then a reference to another "node", which is the next in the list. 

#### Traversing
Linked lists need to be traversed to find elements (generally with a while loop), i.e.,
```java
Node current = this.head
while(current != null) {
	System.out.println(current.data);
	current = current.next;
}
```
#### Adding 
Adding is easy, especially to the tail in a base linked list class, but you must be careful about maintaining links.

###### Adding to the Tail
1. Link the tail node to the new node. 
2. If we keep a reference to the tail of the list, move the reference to the new tail
###### Adding to the Head
1. Link the newly added head to the head of the list.
2. Change the head reference to the new node

##### Adding to the Middle
1. Link the new node to the target of the previous node (the one it is "pushing forward")
2.  Link the previous node to the new node

#### Removing

###### Removing the Head Node
1. Save a link to the old head
2. Update the head reference to the next node
3. Remove the link joining the old head to the new head

#### Maintaining a Tail Node
Maintaining a tail node is more efficient as it makes adding a new tail O(1)
###### Adding a Tail
1. Link Tail to the new node
2. Update the Tail reference

#### Efficiency
A linked list with a head and tail node is O(1) for operations adding to either end, O(n) for operations in the middle, and O(n) for finding items. It is O(n) in space complexity (usually size of the address. So 64-bit system = 8bytes)
## 2. Doubly Linked List
This helps with operations such as finding the second to last item, or removing the tail, which otherwise would both be O(n) operations. In this, a node maintains a reference to both the previous node and the next node.

#### Adding
###### Add to Head
1. Link New Node to Head
2. Link Head back to new node
3. Update Head Reference to new node

###### Add to Tail
1. Link Tail to new node.
2. Link the new node to the  old Tail
3. Update Tail ref to new node
#### Removing
###### Remove Head
1. Save link to Old Head
2. Update Head Ref to next
3. Sever link***s*** between old and new

###### Remove Tail
1. Save link to Old Tail
2. Update Tail Ref to prev
3. Sever link***s***  between 

#### Efficiency
O($n^2$) for space efficiency. 
## Iterators
To avoid accidentaly O($n^2$), most languages support iterator objects that store information about the current state (which node they're on, etc) while the data is read sequentially.
Iterators are O(n) for access. An example is the for-each statement.

## Comparison
![[Screenshot 2023-10-02 at 5.16.49 PM.png]]


