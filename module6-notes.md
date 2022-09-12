# Object-Oriented Programming (C++) I
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

------

## Lecture 1: Object-Oriented and Class Definition

_Definitions_

> **Object-Oriented Programming**: uses data in objects of manipulation; focuses on data being manipulated
> and all manipulations are grouped together in an object.
> 
> **Abstract Data Types**: class; encapsulation of state in an object that can only be accessed through
> operations defined on them
> 
> **Inheritance**: extending a class by keeping the unchanged parts and allowing the objects to use
> functions from the parent class (yay reusability)
> 
> **Class**: A blueprint
>
>  **Object**: An item built from the blueprint

------

The focus-feature of OOP is classes and objects. A class is a full-fledged type:
- can have variables of a class type (_objects)
- can have parameters of a class type
- can be used like any other type

------

## Lecture 2: Member Functions

Classes allow two member types:
1. Description of state (internal variables)
2. Operations (functions)

Functions can either be in-class or out-class:
- _In_: inside the original class; good for short functions (e.g., getters and setters)
- _Out_: outside of the class; generally longer; use the _Scope Resolution Operator_ (SRO) - `class_name::function_name`

It is a good practice to divide a class into header and source files:
- _Header_: class definition (`class.h`)
- _Source_: function implementations (`class.cpp`)

------

## Lecture 3: Access Modifiers / Information Hiding

_Definitions_

> **Information Hiding**: segregates the design decision to make information in a class publicly
> available or limit its access only to members within the class
> 
> **Data Abstraction**: details of how data is manipulated within a class not known to user
> 
> **Encapsulation**: bring together data and operations, but keep "details" hidden

------

There are three levels of data access in `C++`:

1. _Public_: accessible by any function
2. _Protected_: accessible by member functions/friends of the class; can also be used by derived classes
3. _Private_: accessible only by member functions and friends

Data members are _almost always_ private. This upholds the principles of OOP to hide data
and forces manipulation solely through operations.

Member functions, however, are _almost always_ public.

------

## Lecture 4: Constructors and Destructors

### Constructors

- Initialization of objects (some or all member variables)
- Special kind of member function that is automatically called upon declaration of an object
- Must have same name as class and CANNOT return anything, even void
- Must be in public section

### Destructors

- Opposite of constructors (automatically called when an objected is out-of-scope or deallocated)
- Default version only removes ordinary variables, not dynamic variables
- Dynamically-allocated variables do not go away until `delete`d
- Needs a `~` at front

------

## Lecture 5: Static Memory

In terms of OS memory management: the OS allocates a piece of memory to each task/program, which is
then further subdivided:

1. _Static_: all global and static local variables
2. _Stack_: all non-static local variables in classes or functions
3. _Heap_: all dynamically allocated variables (via `malloc` or `new`)

![Image of memory partitioning](/images/memory-partition.PNG)

Static memory is:
- allocated during compilation (before execution)
- there is only one copy of the memory
- changes make to a static variable impact _ALL_ functions and objects that use that variable
- static variables only go out-of-scope when the program terminates

Advantages:
- Variable declaration is in same place of usage (readability)
- Prevents other functions from accessing it

------

## Lecture 5: Stack and Heap Memory

All non-static local variables come from the stack.

Ex:

```c
void main(void) {
  int i = 0;
  i++;
  i = foo(i);
}
int foo(j) {
  int k = 2;
  j = j+k;
  return j;
}
```

![Stack memory example](/images/stack-memory-example.PNG)

Heap, on the other hand, is used for dynamic memory allocation.

Ex:

```c
class contact {
  char name[30];
  int phone;
} contact *p = new contact();  // dynamically allocated - comes from heap
```

There is a big difference when it comes to scope. When an object goes out-of-scope:
- _Stack_: automatically popped out of the stack and memory is freed
- _Heap_: must be _EXPLICITLY_ freed; otherwise, you'll just hold onto that memory

------

## Lecture 6: Garbage Collection

_Definitions_

> **Garbage**: Memory that was once allocated to the program but cannot make use of that memory anymore

------

Java does automatic garbage collection.
- **Pros**: Programmer doesn't have to deal with it.
- **Cons**: Does not run that often. It may come too late or at a bad time.

C++, on the other hand, does not do garbage collection automatically. Programmer has to do it.

- Memory leakage: programmer forgets to delete unused objects, causing the program to run out of memory
- Dangling reference: trying to access an object that has been deleted or out of scope

Best practice: Every `new` operator _SHOULD_ have a matching `delete` operator.

------

## Lecture 7: Deleting Collections of Objects

This lecture covers the best way to delete common collections of objects:

- Linked List: Use a loop and temporary pointer to delete each node forwards, one by one
- Tree: Using postorder, delete each node one by one
- Array: Delete the array using `delete[] p;`

------

**NOTE**: Lecture 8 is examples of memory leak detection. Better to watch this one.
