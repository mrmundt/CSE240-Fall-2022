# Imperative Programming (C & C++) II
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

## Lecture 1: Basic Pointers - The Concept

_Definitions_

> **Value**: Stored in a variable (e.g., a book)
> 
> **Location**: Where a value is stored (e.g., a place on a bookshelf)
> 
> **Address**: Use by human/machine to access a memory location where a value is stored (e.g., floor + shelf + location number)
> 
> **Name**: Self-explanatory, but note, not all locations have a name (e.g., name of book)
> 
> **Pointer**: Also a variable; has value, location, address, and name (e.g., catalog entry with
> a book address, an entry in a database, index associated with the location, and location with name)
> 
> **Pointer type**: Using a variable to store an address
> 
> **Referencing**: Obtain the address of a variable from its name (`&` operator)
>
> **Dereferencing**: Returns value pointed at by a pointer (`*` operator)
>
> **r-value**: If `y = &x;`, then `&x` is the r-value; must happen on the right side of an assignment
> 
> **l-value**: returns a value at an address (e.g., if `*y = 5`, `*y` is the l-value); can be on left or right side

------

Variable names bind physical memory address to a human-readaoble symbol.
We can use addresses to manipulate data (called _direct manipulation of addresses_). This
lets us construct large collections of data and access them from anywhere.

**CAUTION**: All variables store a value at some address; sometimes the value at that address is itself an address.

In `C` Notation, there are two operations on a pointer value:
- Address value can be assigned to a pointer variable
- Address stored in a pointer variable can be modified

This can be done via referencing and dereferencing.

### Box and Arrow Notation

A _box_ represents a storage location whereas an _arrow_ represents the value in a location.

![Example: C code](/images/box-arrow-1.PNG) ![Example: Box and arrow notation](/images/box-arrow-2.PNG)

------

## Lecture 2: Pointer Tracing

We start with an example of how to trace references and dereferences:

```c
int y = 10;   // normal declaration
int* yptr;    // Create a pointer
int *xptr;    // Create a second pointer (* placement doesn't matter)
yptr = &y;    // Address of y into yptr
xptr = &y;    // Address of y into xptr
*yptr = 20;   // Dereferencing: y now equals 20
*xptr = 30;   // Dereferencing: y now equals 30
```

Another example (assume the address of `x` is `2000`):

```c
int x = 500, *y;   // x = 500, y is... Something random
y = &x;            // x = 500, y = 2000
*y = 100;          // x = 100, y = 2000
y = y + 100;       // x = 100, y = 2040 (NEW ADDRESS)
*y = 100;          // x = 100, y = 2040 - but the value at 2040, whatever it was before is now 100
```

One last example with lots of nested references:

```c
int i = 137, *j, **k;
j = &i;               // Address of i
k = &j;               // Address of address of i
**k = 0;              // Now i = 0!
```

------

## Lecture 3: String Usage

_Definitions_

> **Compound Data**: Data that is made of different pieces (e.g., `struct` or `class`)

------

A pointer can point to a variable of any type, and it is especially common for complex/compound types.
This is because a pointer gives us the _START_ of some region.

Ex:

```c
void main() {
  char *p = "hello", *s = "this is a string";
  p = s; // p is now "this is a string"
}
```

The strings above are created implicitly. The syntax creates the strings as arrays in memory and saves the
address of where the array starts as the pointer value. That is, `p` and `s` are simply addresses of the
_FIRST_ character in the array.

Array version:
```c
void main() {
  int n = 0, len;
  char str[] = "hello world";
  len = strlen(str);
  for (n = 0; n < len; n++)
    putc(str[n], stdout);
  printf("\nn = %d\n", n);
}
```

Pointer version:
```c
void main() {
  char *p = "hello world";
  while (*p != 0) {
    putc(*p, stdout);
    p++;
  }
  printf("\np = %d", *p);
  printf("\np = %d\n", p);
}
```

Using pointers is sometimes faster than arrays:
- _Array_ internally looks like `str + sizeof(entry)` to access `str[n]`
- For _Pointers_, `p` is a direct address. Moving forward is simply addition.

------

## Lecture 4: Multi-dimension Arrays

There are **TWO** ways a multi-dimension array can be structured in memory:
1. If static (e.g., all dimensions known in advance): Memory is _contiguous_. The name of the array is
   the initial address of the entire multi-dimensional array.
   
   ![Contiguous memory](/images/contiguous.PNG)
   
1. If dynamic (e.g., size defined at runtime): Memory is _fragmented_. The name of the array is
   the initial address of a series of addresses that lead to each other partition.
   
   ![Fragmented memory](/images/fragmented.PNG)

**NOTE**: `C` uses _row-major_ order, that is, rows are stored one after another.

------

## Lecture 5: Pointer Types vs. Unsigned Ints

_Question_: Are pointer types and unsigned integers equivalent? What is the difference?

_Answer_: Addresses have real-valued representations. You can move forward or backward one "house", but we cannot
divide or multiply. In other words...

- Both have the same range
- Both support `+` and `-`
- Pointers do _NOT_ support `*` or `/`

------

## Lecture 6: String Literals

_Question_: What is the difference between a string as an array and strings associated with a pointer?

_Answer_: Primarily, the difference is mutability. Pointers are constant/immutable.

Ex:
```c
void main() {
  int i = 0;
  char a[] = "my personal password is 1a2b3c", b[22];  // array
  char *p = "send me your password", *b;               // pointer (constant/immutable)
  while (a[i] != "/0")
    a[i] = *(a + i++) + 1;
}
```

`p` and `q` in the above example are _constant string literals_ and may not be changed. 

------

**NOTE**: Lecture 7 is mostly examples. Better to watch this video.

------

## Lecture 8: Defining New Types - Constants

There are two mechanisms for constants in `C`/`C++`:
1. _Macros_: compiler substitutes values for constant definitions (faster execution)
2. `const`: May be a "variable" that is the program is not allowed to modify (slower; must read memory)
    (**NOTE**: This _can_ be manipulated by pointers, but not a good idea.)

A constant defined by `const` is a variable - it has allocated memory, `&` finds the address, and can be modified.

A constant defined as a macro can **NEVER** be modified.

------

## Lecture 9: Typedef and Enum

_Definitions_

> **typedef**: This keyword introduces a new name that becomes a synonym for the type given
> by the type name portion of the declaration (e.g., `typedef int boolean` -> `boolean x = 0`)
> 
> **enum**: This keyword allows us to define a type that is to be populated by specific elements
> or symbols (e.g., `enum {false, true} boolean` -> `enum boolean x = false`)

The two together can make things very easy: `typedef emum days Days; Days now = Mon`

------

## Lecture 10: Composite Data / Structures

_Definitions_

> **struct**: This keyword allows us to creature a structure or a composite data type.

Ex:

```c
struct type_name {
  type1 element1;
  type2 element2;
  ...
  typen elementn;
}
struct type_name a, b;
a.element1 = 10;
```

------

**NOTE**: The remaining lectures in Module 3 were demo videos on how to create a Contact Manager in `C`.

