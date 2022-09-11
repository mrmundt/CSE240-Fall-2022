# Programming Paradigms
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

## Lecture 1: Aspects of Programming Languages

_Definitions_
> **Algorithm**: well-defined, step-by-step, that can be executed on a computer (also known as __Computational Problem Solving__).

------
We can choose a language or group of languages based on their problem-solving technique (e.g., top-down, bottom-up, recursive).
A certain _paradigm_ supports a style of programming or problem-solving.

But _why do we care_? Because of ways to express ideas, choose appropriate languages, learn new languages, design new languages.

### Metrics of Language Evaluation

1. When computing was hardware-limited, we cared entirely about _efficiency_ and usage of (ideally less) memory
2. As computers became faster, programmers also needed to be fast, so we started to care about _writeability_.
3. Now we care about the 3 R's: _Readability_, _Reusability_, and _Reliability_

![Tradeoff Matrix](/images/tradeoff-matrix.PNG)
-------

## Lecture 2: Development of Programming Languages

_Definitions_
> **Program**: a sequence of instructions in memory
> 
> **CPU**: Computing processing unit; interprets the sequence in order
> 
> **Lowest level**: Sequence of bits of machine code

------

1. Early languages were limited by hardware. Thus, emphasis was on _efficiency of execution_.
1. Compiler technology allowed for more complicated tasks and BIGGER problems. This led to the importance of the "ilities".
   Programs were always thought of in a "data in -> program -> data out" format. This is from the 1940's and is known
   as the **Stored Program Concept** or **von Neumann Machine**. Lowest level functionality led to the need for
   an _assembly language_ to translate into machine code.
1. Programs got bigger! So we needed a higher level language (e.g., Autocode - Manchester Mark I, 1952)
1. _Structured Programming_ (e.g., Pascal, C) came into the picture. This allowed for more abstraction,
   to focus on the structure itself (factoring the code into smaller pieces), scoping of variables,
   and better scopes for procedures.
1. _Object-oriented programming (OOP)_ was next. This allows for "bottom-up" problem solving. It introduced even
   MORE abstraction, as well as reusability through inheritance.
1. _Parallel Programming and Distributed Computing_ came next, which allows for multi-processing and threading.
1. _Service-oriented programming_ came last. It's a mix of OOP and web technology. (e.g., XML, OWL, WSDL)

-------

## Lecture 3: The Paradigm Concept

_Definitions_
> **Paradigm**: Example or pattern; a model
> 
> **Paradigm** (in CS): A coherent set of methods that are effective in handling a given type of problem
> 
> **Paradigm** (in Programming): Basic principles of how a computation or algorithm is expressed.

------

There are **TWO** approaches to programming:

1. _Imperative/Non-declarative_: There is a focus on **HOW** to execute.
   - Defines control flow as statement to change state
   - The algorithm is explicit; the goal is implicit
   
   Ex:
   
   ```c
   int func(int n) {
     int t = 1;
     while n > 0 {
       t = t*n;
       n = n-1;
     }
     return t;
   }
   ```
1. _Declarative_: There is a focus on **WHAT** to execute.
   - Only program logic; flow is generated during execution
   - The goal is explicit; the algorithm is implicit
   
   Ex:
   
   ```pascal
   fun fac(0) = 1
   |   fac(n) = n*fac(n-1)
   ```

### The Four Major Paradigms

![The Four Paradigms](/images/prog-paradigms.PNG)

1. _Imperative/Procedural_ (Non-declarative): Fully specified and controlled manipulation of named data in a step-wise function
   - Ex: `FORTRAN`, `C`
   - Sequence of statements and procedural definitions
   - Top-down problem solving
1. _Object-Oriented_ (Non-declarative): Encapsulation of state in the program objects (accessed through operations defined on them)
   - Ex: `C++`, `Python`
   - Objects contain both data and code
   - Program is a sequence of class and object definitions
   - Bottom-up problem solving
1. _Functional_ (Declarative): A higher level of abstraction, free from programming detail, with simpler semantics and generally closer to mathematics
   - Ex: `Haskell`, `Scheme`
   - Based on _Lambda Calculus_
   - Collection of function definitions
   - Treats computation as evaluation of math functions
1. _Logic_ (Declarative): A set of facts about objects, rules about objects, and the definition/question of relations between objects
   - Ex: `Prolog`
   - Goal is to get rid of programming altogether
   - Based on _First Order Logic_
   - Collection of predicate definitions
   - Rule-based approach to problem solving

There is a fifth, which is called _Service-oriented_:

![Service-oriented paradigm](/images/service-oriented.PNG)

------

## Lecture 4: Structures and Error Types - Lexical

_Definitions_
> **Structure of Programs**: This helps humans and computers agree on code behavior and ensures a compiler can process output

------

There are **FOUR** layers of structure:
1. _Lexical_: `begin` `...` `end`; `{...}`; `;`
2. _Syntactic_: `if...then`, `switch`, `for...do`
3. _Contextual_: variable, type, name, initialization
4. _Semantic_: meaning and execution behavior of a program

### Lexical

"Tokens" are the building blocks of a program. The different "token" types include:
- Identifiers: programmer chosen names
- Keywords: built into the language
- Operators: `+`, `<<`
- Separators: `,`, `;`, `()`
- Literals: numbers, chars, strings
- Comments: `#`, `//`
- Layout / Space: some languages have formatting considerations (e.g., `Python`)

The compiler itself has something called a _lexer_ to find and interpret the tokens.
This is the first step before more complicated actions can happen.

Ex:
```c
int a, b, c; // KEYWORD, IDENTIFIER, SEPARATOR, IDENTIFIER, SEPARATOR, IDENTIFIER
c = 2 * a + b;
```

------

## Lecture 5: Structures and Error Types - Syntactic

_Definitions_
> **Syntax**: describes how to put lexical units together to form valid sentences/statements

------

In the late 1950's, the _Backus-Naus Form_ (BNF) concept was created. This concept represents a 
concise and formal way of expressing syntax. It acts like a meta-language for describing languages.
That is, it describes _context-free language_ (CFL) and _context-free grammar_ (CFG).
A BNF description contains two symbols:

1. _Non-terminal_: represent an "idea" to be decomposed; they don't appear in the final sentence (e.g., a "noun")
2. _Terminal_: appear in the actual sentence - no grammatical rules apply (e.g., "cat" - replacement of "noun")

Ex:

```
<sentence>  ::= <subject> <verb> <object>
<subject>   ::= <adjective> <noun>
<adjective> ::= <adjective> | <adjective> <adjective>
<object>    ::= <subject>
<noun>      ::= table | horse | computer
<adjective> ::= big | fast | good | high
<verb>      ::= is | makes
```

The _syntactic_ layer is the second layer. A compiler breaks code into lexical tokens and then checks against
the syntax rules (BNF).

------

## Lecture 6: Structures and Error Types - Syntax Graphs

A language can also be described using a _syntax graph_.

![Example syntax graphs](/images/syntax-graph.PNG)

------

**NOTE**: Lecture 7 was a case study. It is better to just watch this.

------

## Lecture 8: Structures and Error Types - Contextual

_Definitions_
> **Contextual**: defines the semantics before dynamic execution (e.g., variable initialization and type checking)

------

This is the third layer of a compiler: is the written code contextually correct?

Ex:

```c
string str = "abc";
int i;
i = i + str; // syntactically correct, but contextually incorrect - type mismatch
```

-------

## Lecture 9: Structures and Error Types - Semantic

_Definitions_
> **Semantic**: the implied meaning of a program

------

Semantic errors **CANNOT** be detected by a compiler. These happen when all previous layers are correct,
but there is invalid meaning (e.g., dividing by zero).

Ex:

```c
int x = 0, y = 5;
int z = y / x; // SEMANTIC ERROR
```

- No formal definition for imperative and OO languages.
- Functional programming languages have formal semantic definition based on the mathematics used (see lambda calculus).
- In logic programming languages, logic expressions are often used for describing the semantics.
 - Semantic languages: e.g., `Prolog`, `RDF` (Resource Description Framework) and `OWL` (Web Ontology Language)

------

## Lecture 10: Error Types

- _Lexical errors_: Compiler can detect all of them.
- _Syntactical errors_: Compiler can detect all of them.
- _Contextual errors_: They include all the errors in variable declaration, variable initialization, and type
  inconsistency in assignment. Compiler implementations may or may not detect all the initialization errors,
  depending on if they compute the initialization expression or not.
  
  Ex: `int x = 5/(3-3); //the compiler may not detect this`

- _Semantic errors_: They include all the errors in the statements that will be executed after passing compilation.

   Ex:
   ```c
   int x;
   x = 5/(3+2); //the compiler may detect this error
   ```

------

## Lecture 11: Processing Methodologies

_Definitions_
> **Interpreter**: a program that translates and executes each statement in the high-level language without translating
>                  all statements into executable code.
> 
> **Compilation**: a program that translates the entire code from source to binary, and then runs.
> 
> **Intermediate**: A code concept implemented in early version of `Pascal` to simplify compiler design.

------

There are **THREE** methods for program processing:
1. _Interpretation_: A program is run by another outside program and simulated (e.g., `Python`)
   - **Pros**: No separate compilation phrase (quick development); good debugging information
   - **Cons**: Slow execution; can use more memory space; big/complex languages are difficult to interpret
1. _Compilation_: Systems where source code -> binary file in one step (e.g., `C++`)
   - **Pros**: Faster than interpretation; good for multi-module programs
   - **Cons**: Separate compilation phase; may lose debugging information
1. _Intermediate_: In `Java`, the language uses an intermediate code to make the language and compiler machine-independent
   - **Pros**: Single compiler for all machines; small VM fits in a web browser
   - **Cons**: Lose information through the conversion; difficult to optimize

------

## Lecture 12: The Macro Concept

_Definitions_
> **Macro-Processing**: substitutes a definition for a name in the program; arguments are allowed for creating in-line functions;
>                       eliminates function-call overhead; occurs in the pre-processing phase

------

Macros are faster to execute, but they make longer machine code.

Ex:
```c
#define AREA_OF_TRIANGLE(b, h) (b*h)/2
int base = 3;
int height = 5;
float area = AREA_OF_TRIANGLE(base, height);
```

------

## Lecture 13: Macros versus Functions in C

This video is full of examples and side-effects. Ultimately, the moral of the story is that macros can be very dumb.
There is absolutely **NO** extra processing that happens. They copy-paste and can have a lot of weird behavior.

Ex:
```c
#define abs(a) ((a<0) ? -a : a)
j = abs(2-5); // j = ((-2-5 < 0) ? -2-5 : 2-5)
j = -7 // WRONG!!
```

------

## Lecture 14: Macro Processing Caveats: Side effects

This video has more examples like above in Lecture 13, but adds a bit.

Macros can vary by compiler. Some macros work in Visual Studio, for example, but are incorrect in `gcc`.

------

## Lecture 15: Example - Manually Applying a Macro

How does this macro expand?

```c
#define MAXVAL 100
#define QUADFN(a, b) a*sqrt(b) + b*b - 2*a*a*t++
x = MAXVAL + QUADFN(5, 16); // x = 100 + 5*sqrt(16) + 16*16 - 2*5*5*t++
```

------

## Lecture 16: Macros versus In-lining

_Definitions_
> **Final Variable**: If a variable is declared `final`, it may not be modified after its initialization (e.g., `final basevalue = 24`)
> 
> **Final Method**: This method cannot be overridden in a subclass

------

Why might one want to declare a variable final?
- Readability (e.g., `final pi = 3.14`)
- Efficiency. All appearances of `basevalue` are replaced by its value by the compiler, which is packed in one machine code.

Why might one want to declare a method final?
- The compiler may optimize by replacing all calls to that method (this is called _in-lining_ the code)

What is the difference between _In-lining_ and _Macros_?
- _In-lining_: compiler decides optimization; compiler responsible for correctness; programmer has no idea if the optimization was done
- _Macros_: programmer decides optimization; programmer responsile for correctness; macros are forced in-lining and the programmer can predict performance
