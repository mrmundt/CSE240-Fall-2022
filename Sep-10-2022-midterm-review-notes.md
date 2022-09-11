# CSE240 Midterm Review - September 10, 2022

## TA: Halle Countryman

Types of programming errors:
----------------------------
- Lexical: The words of your program - var names, symbols, keywords
- Syntactic: The rules for putting the words together - Backus-Naus Form (BNF)
- Contextual: Variable initialization and type checking (can be confused with semantic)
- Semantic: How do your intentions differ from the actual functionality of the program? (user-error);
            "I think of Semantic errors as errors that occur when your compiler follows the logic
			you've set out for it, but it doesn't give you your desired output."

Backus-Naus Form (BNF)
----------------------
Remember, this is the syntactical rules. Be prepared to be able to read a BNF
and find those examples that are valid.

Recursion: The nth fibonacci number
-----------------------------------
The four steps of recursion:
1) Size-n problem (as in, the most generic, high-level thing)
   ex: "What is the nth fibonacci number?" - `int fib(int n)`
2) Find the stopping condition and corresponding return value
   ex: "The 0th Fibonacci number is 0; the 1st is 1"
3) Formulate the m-size problem - that is, the smaller problem (`m1 = n-1`, `m2 = n-2`)
4) Construct the solution of the size-n problem from the size-m
   ex:
   ```
   int fibonacci(int n) {
     if (n <= 1) {
	   return n;
	 }
	 return fibonacci(n-1) + fibonacci(n-2);
   }
   ```

Tail recursion: A recursive function that calls itself only ONCE or in the last statement.
   ex:
   ```
   int fib(int n, int x, int y) {
     if (n == 0) return x;
	 if (n == 1) return y;
	 return fib(n-1, y, x+y);
   }
   ```
   // Initial call: `fib(n, 0, 1)`
   If n = 4:
   `return (3, 1, 1) -> return (2, 1, 1) -> return (1, 2, 3) -> return 3 // STOPPING CONDITION`
   
Constants
---------
- A "variable" that does not change (allows for compiler optimizations)

Q: Can you change one?

A: Technically, yes, if, to quote Lee, you're using "pointer trickery".
   You can use pointers to directly access the memory where `const` is stored.

BUT NOTE. This is different from a macro! This is a literal substition for a value.

ex: `#define MAX_STUDENTS 10; // but you must know the value in advance`

Macros
------
What are the differences?
- Regular functions: seen by the compiler; uses the stack to store local variables
- Macros: just copy-pasta'd into the code (pre-processed; eliminates function-call overhead);
          programmer decides the optimization and is responsible for correctness.
- Inline: Does not use the stack, but unlike macros, any params will be evaluated only once.
          This keyword is a SUGGESTION, though, to the compiler. It may inline things without
		  asking to optimize your code.

Make sure to know how to do macro substitution / identifying side effects.

Pointers
--------
- r-value: `&var` - the address at which the variable `var` lives (`y = &x`)
  
  (NOTE: `&` <- is for referencing/obtaining the address of a var from its name)
- l-value: `*var` - the value at the address stored in the variable `var` (`*y = 5`);
           When it is on the left-hand side, it can be a declaration pointer or derefence operator.
		       On RHS, it'll always be the dereference operator.
  
  (NOTE: `*` <- is for dereferencing/returns the value pointed at by a pointer)

But what is array syntax (`arr[]`) really?
Essentially, syntactic sugar that boils down to the same assembly as pointers would.
   ex:
   ```
     arr -> &arr[0] : Array at address 0
     char *arr -> char arr[] : allocates the array brackets syntax as stack memory
     *(arr + 4) -> arr[4] : Dereferencing the address plus four; increments the element of the array/address
   ```

C strings
---------
- A string in C is an array of chars with `\0` at the end (e.g., null terminator).
 
  WARNING: If you try to manually make a string or mess with your string and get
           rid of the null terminator, C will not like that. The program will keep
		       looking until a null terminator just happens to be found in memory somewhere.

Parameter passing
-----------------
- Call-by-value: Creates the new memory on the stack and copies the value of the parameter
               into it, so the outside reference does not change.
- Call-by-address: Call the value of a pointer and then dereference it with a * to modify
               values outside the stack.
- Call-by-alias: param must be a variable rather than a literaly, alternative to call by address
   - Cannot pass a constant
   - Involves one variable only (call-by-address uses two)
   - Uses var name `n` in function (`*n` in call-by-address)


Freeing memory
--------------
When would you use the following:
- free() : C/C++ function ; after using `malloc` keyword
- delete : C++; after using `new` keyword
- delete [] : C++; for arrays; after using `new []` to make an array

Struct padding
--------------
Padding: optimization for performance that aligns struct members on word boundaries;
         you can optimize for size on some architectures but performance will suffer;
		 "For the size of a member which is not a multiple of its size, the extra
		 spots must be filled to align the data."
Rules:
1) Each member of a struct gets padding before it so that it can begin on an address
   divisible by its size (e.g., a short int of 2 bytes will start on a boundary that's
   a multiple of 2, an int size of 4)
2) You have to fill up at the end, too - and it must be divisible by the largest member.

Ex: (x86_64) - Know the byte values at least on 32-bit systems
```
struct foo {
  char a;          // 0   a: 1 (needs 1 padding)
  short int b;     // 2   b: 2
  char c[3];       // 4   c: 3 (needs 1 padding)
  int d;           // 8   d: 4 (needs 4 padding)
  struct foo *e;   // 16  e: 8 (pointers are long ints)
  char f;          // 24  f: 1 (needs 7 padding so we reach something divisible by 8)
}                  // total: 32 bytes
```

Memory layout
--------------
- Stack: the memory used by local function-scoped vars (compiler handles this)
- Heap: dynamically allocated memory (user manages this)
- Static: the memory used for global and static variables (statics are block-scoped)
- Text section: stores the actual machine instructions
