# Typing and Imperative Programming (C & C++) I
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

## Lecture 1: Types and Orthogonality

_Definitions_

> **Data Type**: defined by a set of primary values allowed and operations on those values; declaration of variables (e.g., `int`)
> 
> **Type Checking**: contextual; process of ensuring that the types of and operands are legal or equivalent to a legal type.

------

## Lecture 2: Data Type Equivalence and Conversion

_Definitions_

> **Structural Equivalence**: two types are equivalent if they have the same set of values and operators
> 
> **Name Equivalence**: two types are equivalent if they have the same name; anonymous types are not equivalent.
> 
> **Coercion**: implicit type conversion (e.g., `float f = 3.14 + x;`)
> 
> **Casting**: explicit type conversion (e.g., `int i = (int)f + x;`)

------

## Lecture 3: Strong Type Checking

_Definitions_

> **Strongly Typed Language**: each name in a program has a single type associated to it; type is known
> at complication time; errors are ALWAYS reported; trades flexibility for reliability

------

Weak type checking can causes contextual errors to become semantic errors.

Note, though, that no language is fully strong or weak. For example:
- `Pascal` is nearly strong-typed. It allows omission of type checking in its variant record.
- `Ada`/`Java` are nearly strong-typed. They allow type checking suspension for a particular type by
   calling `UNCHECKED_CONVERSION`
- `C++` is less strongly typed, and `C` even less so.

------

## Lecture 4: Basic I/O - Introducing C

_Definitions_

> **Imperative Paradigm**: Features fully specified/controlled manipulation of named data in a step-wise fashion;
> abstractions of a von Neumann machine; algorithmic in nature - _how_ rather than what; popular due to performance
> and culture.

------

The basic building blocks of `C`/`C++`: Functions!
- Built-in are pre-written and exists in libraries
- User can define their own
- Functions may exist outside any class in C++ and variables may exist outside class/functions. These are called _globals_
- Each `C`/`C++` function may contain exactly _ONE_ `main()` function

The `main()` Function
- Simplest examples: `main() {}` <- generic; `void main(void) {}` <- takes in and returns nothing; `int main() {return 0;}` <- uses a success code
- Can add certain parameters to allow for command-line outputs: `void main(int argc, char* argv[]) { ... }`

-----

**NOTE**: Lectures 5-7 were geared towards setting up a computing environment. Notes not helpful.

-----

## Lecture 8: Formatted I/O

_Definitions_

> **Expressions**: list of expressions whose values are to be printed out; comma-separated
> 
> **Control sequence**: helps with type evaluation; includes string to be printed and control symbols

------

This lecture deals with providing input and receiving output.
1. _Input_: `scanf(control sequence, &var_1, ..., &var_n)  // & tells address of a var`
2. _Output_: `printf(control sequence, expressions)`

In `C`, the different printable types are:
- `%d` : `int`
- `%f` : `float`
- `%c` : `char`
- `%s%`: `string`

-----

## Lecture 9: Unformatted I/O

The basic idea here is to treat data like a stream of bytes. In c-style:
- `fgets()` reads until a size is reached, a new line occurs, or the end of a file.

   `fgets(var_name, sizeof(var_name), stdin) // where to store, how many spaces, from the keyboard`

To summarize:
- _Unformatted_ reads `char`s and `string`s. This list includes: `getchar`, `putchar`, `fgets`, `cin.get`, `cin.getline`
- _Formatted_ reads `char`s, `int`s, `float`s, etc. This list includes: `scanf`, `printf`, `cin`, `cout`

------

## Lecture 10: Imperative Data

_Definitions_

> **Declaration**: binds a name to a location in memory and describes the attributes of the value in the location
> (_Type_, _Scope_, _Qualifier_). Normally memory is allocated upon declaration.

------

Data in `C` is viewed _algorithmically_. It is represented by different _states_ (e.g., collections of variables and their values):
1. _Type_: what values and operations are allowed
2. _Location_: where data are stored in (physical) memory
3. _Address_: an integer associated with a location
4. _Reference/Pointer_: a name associated with a variable that holds an address of a location
5. _Variable name_: a name associated with a location
6. _Value_: what is actually stored in a memory location
7. _Scope and visibility_: how we can access the data

------

## Lecture 11: Scoping Rules

_Definitions_

> **Scope Rule**: the scope of the variable starts from its declaration point and extends to the end of the current block
> 
> **Forward Declaration**: a name is known before it is used. _NOTE_: A program cannot use a name before it is defined.

------

## Lecture 12: Primitive Types

`C` has 5 basic types:
- `char`
- `int`
- `float`
- `double`
- `void`

`C++` adds two more:
- `bool`
- `wchar_t` (wide `char`)

These can also have modifiers added onto them: `signed`, `unsigned`, `long`, and `short`

![Chart of C and C++ ranges](/images/primitive_types.PNG)

![Hierarchy of data types](/images/data_hierarchy.PNG)

-----

## Lecture 13: Memory Organization

This lecture is best described by the images presented. There are two important notes:

- Memory is _byte-addressable_: the address of something larger than `char` must be multiples of 4 for performance
- Each system has a _word size_: a fixed size unit of data that can be processed natively

![Memory hierarchy and access time](/images/memory-hierarchy-access.PNG)

![Example: Olympic Game Hotel and Transporation](/images/olympic-game-example.PNG)

------

## Lecture 14: Byte Addressable Memory

_Definitions_

> **Byte Addressing**: hardware architectures that support accessing individual bytes of data rather than words;
> allows quick access to data within system memory.

-----

The video has an example which is described as "looking a little bit to the side" of the original address.

------

## Lecture 15: C-style Strings

_Definitions_

> **C-style string**: array of chars that terminates with a null character. This has two meanings: an array of chars and a string.
> 
> **Array** collection of data elements that all share the same type and accessible by index.
> 
> **Truncated Init**: size of array is specified and there is not enough space; null char will **NOT** be attached to the string.
> Ex: `char s[5] = "alpha"; // [a][l][p][h][a], no null character to terminate`

-----

There are two ways to initialize an array of chars:
1. `char s[] = {"a", "l", "p", "h", "a"}; // array of chars - will not include the null character`
1. `char s[] = "alpha"; // string - will include the null character [a][l][p][h][a][/0]`
