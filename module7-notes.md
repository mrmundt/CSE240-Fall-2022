# Object-Oriented Programming (C++) II
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

------

## Lecture 1: Inheritance Basics

_Definitions_

> **Inheritance**: define new calsses by extending existing classes

-------

All OOP supports:
- new class inherits existing members
- may add members
- may redefine members

In terms of scope, though:
- _Private_ variables are reserved for base class
- _Protected_ variables can be used by derived classes
- _Public_ variables can be used by ALL classes in the project

------

## Lecture 2: Class Inheritance and Hierarchy

_Definitions_

> **Multiple Inheritance**: a derived class that inherits members from more than one base class.
> _USE WITH CAUTION._

------

Inheritance doesn't have to stop after one derived class. You can keep going in a layered hierarchy.

Best practices:

1. Place all common fields/operations in the base class
2. Placed shared objects as high as possible
3. Distinct objects should be placed in derived class
4. Override/Redefine: subclass can redefine a field or operation if it is a _virtual_ class

-----

## Lecture 3: Polymorphism

_Definitions_

> **Polymorphism**: allow some fields/operations to behave differently in different contexts.
> 
> **Dynamic/Late Binding**: for use in virtual members; creates a pointer to the corresponding
> function in the base class. Pointer is not assigned to a specific function at compile time;
> rather, assigned at runtime.
> 
> **Overloaded Functions**: same name, different parameters (in type or member). Can be applied
> to constructors and normal functions, but must have same return type.
> 
> **Virtual Functions**: same parameter list and return type, different implementation.

------

A pointer cannot access derived class fields or operations without explicit type casting.
C++ pointers are essentiall static. Polymorphism only allows you to use the common
field or operations where the compiler will not see the difference.

------

## Lecture 4: Containment

_Definitions_

> **Containment**: placing a class object within a class ("has-a" relationship)
> 
> **Inheritance**: base class is a template; derived class adds new fields/operators ("is-a" relationship)
> 
> **Value type/semantics**: (in imperative languages) all data can be accessed through a
> named variable; may have a pointer pointing to a variable (**)
> 
> **Reference type/semantics**: (in OOP) all data are objects and all objects have to be accessed
> by a reference (pointer) (##)

---------

When do you use _Containment_ versus _Inheritance_?

| Inheritance | Containment |
| ----------- | ----------- |
| "is-a"      | "has-a"     |
| manager "is-a" employee | car "has-a" tire|
| priority queue "is-a" queue | student "has-a" course |

(**) The name can be used on the left or right side of the assignment; compiler will associate
variable name to memory address; may associate >1 name to one memory address ("alias");
when parameters are passed using pass-by-value, the data value/object is passed.

(##) There is a clear distinction between variables and the object it names; data accessed
through a reference variable; multiple reference variables pointing to the object cause
memory overhead; when parameters are passed using pass-by-value, the reference to
the object is _actually_ passed.

------

## Lecture 5: File I/O in C++

_Definitions_

> **Stream**: a flow of characters; input -> program; output <- out of program

Input streams:
- `cin` - input from keyboard; `ifstream` - read from files
- `cout` - output from program to terminal; `ofstream` write to files

------

## Lecture 6: Input Buffer

Buffers are located in memory. An _input buffer_ is an invisible array to capture keystrokes
from the keyboard. In `C++`: `cin`, `cout`, `cin.get`, `cin.getline`, `cin.ignore`

------

**NOTE**: Lecture 7 was an example. Better to watch it.

------

## Lecture 8: Exception Handling

_Definitions_

> **Exception**: a (forced) deviation caused by a(n) (un)known event from the normal
> execution sequence of the program
> 
> **Internal Exception**: e.g., divising by 0; software-related; comes from within the CPU
> 
> **External Exception**: e.g., out-of-memory; comes from outside of the CPU

------

### Exception Handling

Exceptions will be handled at different levels:

- _Hardware level_: When an exception occurs, the hardware identifies the exception source and computes the exception handler's entry address.
- _OS level_: For each exception, a simple exception handler is provided that is stored at the specified handler's entry address.
- _Programming language level_: The language provides exception classes to handle the exceptions with more details.
- _User program level_: A programmer can write application-specific exception handler to handle the exceptions. It is better to separate the
  code that perform required functions from the code that handle the exceptions.

### C++ Exception Statements (SYNTAX)

```
<exception-structure> ::= try <code-block> <handler-list>
<handler-list> ::= <empty> | <handler> | <handler-list> <handler>
<handler> ::= catch ( <except-declaration>) < code-block >
<except-declaration> ::= <type-name> |
<type-name> <identifier> |
<type-name> *<identifier>
<throw-statement> ::= throw | throw <expression>
```

Note: a throw statement is similar to a return statement. It exits out of that block of statements.
