# Imperative Programming (C & C++) III
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

------

## Lecture 1: Structure Padding

_Definitions_

> **Padding**: For the size of a member which is not a multiple of 4, the extra spots must be filled to align the data.
> _NOTE_: It does not HAVE to be 4. It's multiples of the data type itself.

------

As a reminder, a `struct` is used to make new data types where smaller types are combined into one larger types.

Then data in these needs to be moved, it is done in chunks the size of a "word" (e.g., 32-bit, 64-bit). This
is for efficiency - it is best if the data is aligned with a boundary so we do only _ONE_ read instead
of multiple.

How much space will this `struct` take up?

```c
struct personnel {
  char name[16];    // 16 bytes
  int phone;        // 4 bytes
  char address[24]  // 24 bytes
  char enrolled;    // 1 byte + 3 bytes of padding
} // 48 bytes total
```

------

## Lecture 2: File Operations

| Disk | Memory |
| ---- | ------ |
| Very large in size | Smaller in size |
| Permanent storage | Data vanishes after restart |
| Slow. Very slow. | Much faster than disk |
| Can read/write in large blocks | Can read/write in bytes or words |
| Sequential access by pointer | Random access by address |

### Buffered Read Access

(_NOTE_: Writing is basically the same but in reverse)

1. Declare a pointer `f` to a `FILE` type
2. Open for reading: create a buffer that can hold a block of bytes
3. Copy the first block of a file into the buffer
4. Program uses the pointer to read the data in the buffer sequence
5. Pointer moves to the end of the buffer, where next block is copied (pointer reset to beginning)
6. Close the file

------

## Lecture 3: Storing a Collection into a File

There are **TWO** ways to store data in a file:
1. Text files: store strings of characters
2. Binary files: store structured data (`int`, `float`)

The most common file operators are `fread` and `fwrite`. They have the following parameters:
1. Memory address (pointer) where source data will be stored into file/destination for read data
2. Number of bytes to read pet item (use `sizeof`)
3. Number of items to read/write (normally 1)
4. The file name to be written/read

------

## Lecture 4: File Access by Position

(_NOTE_: These concepts are old-school and based on tape, not modern technology.)

Since files are represented by sequential regions of data, it is common to access them by "position".
For reading, the file pointer moves automatically after each access.

There are functions that allow you to change the pointer position to access data you want.

### Useful Functions

- `int fseek(FILE *f, long offset, int opt)`: Moves a pointer to a certain position
   - Has multiple uses (find index, jump deeper, etc.)
   - Has optional parameters that can be used for efficiency:
     - `SEEK_SET`: offset relative to beginning
     - `SEEK_CUR`: offset relative to current position
     - `SEEK_END`: offset relative to end 
- `void rewind(FILE *f)`: Reset the file poiinter to the beginning of the file
- `long int ftell(FILE *f)`: Return current pointer position of a given file `f`

------

## Lecture 5: Understanding Buffers

_Definitions_

> **Buffer**: An invisible array variable of bytes or chars (can lead to odd behavior)

------

The video has good animations to describe this. The basic gist is that buffering formatted I/O
is better at getting the right inputted data without extra work. For unformatted I/O, though,
we should flush the buffer between input statements: `fflush(stdin)`

That is also basically the entire content of **Lecture 6**.

------

## Lecture 7: Parameter Passing - Data Flow

_Definitions_

> **Function/Method**: a named block of code that must be explicitly called
> 
> **Abstraction**: statements that form a conceptual unit
> 
> **Reusability**: statements that can be executed in more than one place in a program
> 
> **Formal parameter**: local variables of the function (at declaration)
> 
> **Actual parameter**: "arguments"; when calling a function

------

Functions communicate with the rest of the program by:
- Changing the global/state variables
- Using parameters and/or return values

Ways to implement parameter passing:
- _Pass-by-value_: A formal parameter is a local variable in the function. It is initialized
  to the value of the actual parameter. It is a **COPY** of the actual parameter, not the original.
  - **Pros**: No side effects (safe and reliable)
  - **Cons**: Less flexible/powerful; can be slow
- _Pass-by-address_: A formal parameter is a pointer to the actual parameter. The address
  will be stored as an entry in the stack frame but may point to both stack or heap memory.
  CAN CHANGE THE OUTSIDE LOCAL VARIABLES.

Not from slides, but a useful infographic:

![Visual representation of the different param passing](/images/pass-by-reference-vs-pass-by-value-animation.gif)

------

## Lecture 8: Pass-by-value and Pass-by-address

### Pass-by-value Data Flow

```c
int i = 1;                  // global var
void func (int m, int n) {  // m, n are formal parameters
  i = 5; m = 3; n = 4;      // i change persists; m, n do not
}
```

### Pass-by-address Data Flow

```c
void func (int *n) {
  *n = 30;             // *n is NOT local
  n = 0;               // n is local
}
```

------

## Lecture 8: Pass-by-alias

This is only available in `C++` - NOT in `C`.

It differs from pass-by-address:
- Parameter must be a variable rather than a literal
- Cannot pass a constant
- Involves one variable only (pass-by-address uses two)
- Uses variable name `n` in function (`*n` in pass-by-address)

------

**NOTE**: Lecture 9 was all examples; better to watch this one.

------

## Lecture 10: Linked Lists - Implementing Nodes

_Definitions_

> **Linked Lists**: Comprised of nodes
> 
> **Nodes**: created using a `struct`; stores a value and a link element

------

How to implement:

```c
#define MAX_LEN 1024
struct ContactNode {
  char name[MAX_LEN];
  int phone;
  char email[MAX_LEN];
  struct ContactNode *next;  // This line makes the link to the next node
}
int main() {
  struct ContactNode *n = malloc(sizeof(struct ContactNode));
  // input stuff
  n->phone = 1337;
  printf("phone: %d", n->phone);
}
```

------

## Lecture 11: Adding to the front

If we have a node with data, we want to be able to add another node. To add to the front:

1. Pointer to a node
2. Pointer to the front most node of a list

```c
struct ContactNode* addFront(struct ContactNode* node, struct ContactNode* front) {
  node-> next = front;   // put the new node at the front
  front = node;          // update front to the new node
  return front;          // return the new front
}
```

-----

## Lecture 12: Traversal

```c
void display(struct ContactNode* front) {
  struct ContactNode* temp = front;  // make a copy
  while (temp) {                     // while temp isn't NULL
    printf(stuff);                   // do whatever
    temp = temp->next;               // move to the next node
  }
}
```

------

## Lecture 13: Remove a Node

```c
struct ContactNode* removeFront(struct ContactNode* front) {
  if (front != NULL) {
    struct ContactNode* temp = front;  // need to make a copy to free memory
    front = front->next;               // Take away the first-most node
    free(temp);                        // good practice to free up the memory
  }
  return front;
}
```

------

## Lecture 14: Retrieving a Specific Node

```c
struct ContactNode* selectByName(char* name, struct ContactNode* front) {
  struct ContactNode* previous = NULL;  // we are actually looking at the node right before
  struct ContactNode* temp = front;     // need to make a copy
  while (temp) {
    if (strcmp(temp->name, name) == 0)  // compare the names
      return previous;                  // found it - so return!
    else {
      previous = temp;
      temp = temp->next;                // go to the next node
    }
  }
  return NULL;                          // didn't find it!
}
```

------
