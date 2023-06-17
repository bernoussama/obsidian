### Data types | Integer types (on most 64bits computers)
---

**Type** | **Storage size** | **Value range**
-- | -- | -- 
char | 1 byte | -128 to 127
unsigned char | 1 byte | 0 to 255
short | 2 bytes | -32,768 to 32,767
unsigned short | 2 bytes | 0 to 65,535
int | 4 bytes | -2,147,483,648 to 2,147,483,647
unsigned int | 4 bytes | 0 to 4,294,967,295
long | 8 bytes | −9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
unsigned long | 8 bytes | 0 to 18,446,744,073,709,551,615


#### Arrays
- A succession of items of the same type in memory
* Declaration:
```c
type var_name[number_of_items]
```
	Where number_of_items is a constant number (not a variable)

* Example:
```c
/* array of 32 contiguous int */
int my_array [32] ;
/* array of 8 arrays of 16 chars*/
char my_array_of_arrays[8][16] 
```

#### Blocks
Blocks or code blocks are sections of code which are grouped together. Blocks
consist of one or more declarations and statements.
Blocks are delimited by curly braces `{` and `}`

- Syntax :
```c
{
	[declaration(s)]
	[statement(s)]
}
```

**Blocks**
> Declarations
Declare variables

>**Statements**
	Executed in order
>> Contains:
>> ● Blocks
>> ● Instructions (assigning values, computing)
>> ● Control structures (conditional statements, loops)


### &
`&var_name`
The address in memory of the variable `var_name`
Example:
```c
p = &c; //p now holds the address in memory of the variable c
```
![[Drawing 2023-06-15 14.36.17.excalidraw]]
