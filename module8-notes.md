# Functional Programming (Scheme) I
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

------

## Lecture 1: Scheme Basics - The Functional Paradigm

Functional programming is more about the **HUMAN** than the machine.

_Characteristics_

- Higher level of abstractions
- Closer to mathematics
- No side-effects (referential transparency, no variables)
- Easier for parallel processing
- Functions are treated as _first-class objects_ - that is, they can be placed anywhere where a value is expected

------

## Lecture 2: Expression Notation

_Definitions_
> **Prefix-p Notation**: Add an open parenthesis before each operator; add a close parenthesis after the last operand of the operation.

Scheme uses _prefix-p_ notation for its operations. That is:

```scm
(+ 3 4)        ; This is the same as 3 + 4 
(+ 3 (* 4 5))  ; This is the same as 3 + 4*5
```

------

## Lecture 3: Getting started with Dr Racket

This video is a tutorial on how to set up and use Dr Racket - just watch this one.

------

## Lecture 4: Playing with Expressions

_Definitions_

> **REPL**: Read-evaluate-print-loop; interactive interpreter that gives an environment that can be manipulated.
> 
> **Primitive Expression**: An expression that evaluates to itself; also called an _atom_.

For prefix expressions, the _leftmost_ element is always the _operator_. The following elements are _operands_ (or parameters).

```scm
(+ 3 4)   ; + is the operator; 3 and 4 are the operands
```

------

## Lecture 5: Environment and Define

_Definitions_

> **Form**: Something we want to evaluate.
> 
> **Global environment**: The collection of things in existence at a particular environment.

We can name expression so they persist within the environment.

_Syntax_: `(define <name> <object>)` where `<name>` is the name and `<object>` to bind to the name.

```scm
>(define pi 3.14159)                   ; bind 3.14159 to the name pi
>(define radius-sq (* radius radius))  ; bind expression to the name radius-eq, only works if radius is defined
```

In the second example, if `radius` is not defined, we will get an `undefined` error: `cannot reference undefined identifier`.

------

## Lecture 6: Evaluating Expressions

_Definitions_

> **Eager Evaluation**: Evaluate everything that can be evaluated; innermost first; all arguments of a procedure first.
> 
> **Lazy Evaluation**: Evaluate only what is needed; outermost first; only evaluate arguments of a procedure if the values are needed.

To evaluate a normal expression (also called an _application_):
1. Evaluate any of its operands that are expressions.
2. Apply the operator to the evaluated expressions.

All expressions return _EXACTLY ONE SINGLE VALUE_.

There are two orders in which to evaluate: _eager_ and _lazy_.

```scm
>(+ (+ 3 5)(* (+ 4 6) (- 5 3)))
; eager: (+4 6), (- 5 3), (+ 3 5) -> (* 10 2) -> (+ 8 20)
; lazy:  (+3 5), (+ 4 6), (- 5 3) -> (* 10 2) -> (+ 8 20)
```

------

## Lecture 7: Procedures

_Definitions_

> **Procedure**: An abstraction for an expression whose operand(s) ha(s/ve) free variables.
> 
> Example: `(define (square x) (* x x))`

_Syntax_: `(define (<name> <params>) <body>)` where `<name>` is the name and `<params>` are the operands.

Naming Conventions
- _Procedures & Variables_: lowercase words with dashes (e.g., `remove-primes`)
- _Global Variables_: surrounded with stars (e.g., `*top-score*`)
- _Predicates_: return a bool; put `?` at the end (e.g., `member?`)
- _Mutators_: procedures that mutate data in a non-functional way; put `!` at the end (e.g., `save-id!`)

------

## Lecture 8: Basic Data Types

- _Number_: includes `int` and `float` (e.g., `2`, `1.03`, `-5`)
- _String_: sequence of characters in _DOUBLE_ quotes (e.g., `"Hello world"`)
- _Symbol_: a _SINGLE_ quote folow by a word (e.g., `'Jim`)
- _List_: A list of elements of _ANY_ type (e.g., `'(3 5 Hi Jim (5 9) "Hello")`) 
- _Boolean_: `#t` or `#f`; can check type with `(boolean? 5) -> #f`
- _Characters_: Put `#\` in front of something to make it a character (e.g., `#\5`)

_NOTE_: Strings can be processed; symbols cannot.

This lecture also included lists of forms that can be used for each data type.
I did not capture them all here.

------

## Lecture 9: Scheme Functions - Making Decisions

We need to introduce logic into our Scheme programs.

The new form: _Cond_ - a conditional; treated like a `switch` statement

_Syntax_
```scm
(cond  (<pred1> <exp1)
       ...
       (<predn> <expn>))
       (else <exp)) ; optional
```

Another new form: _If_

_Syntax_
```scm
(if <predicate> <consequence> <alternative>)
```

------

## Lecture 10: Defining a Recursive Procedure

How do we implement `factorial` in Scheme?

```scm
(define factorial (lambda (x)
  (if (= x 0)
       1
       (* x (factorial (- x 1))))))
```

_NOTE_: You do **NOT** get overflow in Scheme. Long numbers can be represented as lists.

------

## Lecture 11: Basic Logic

A list of basic logic functions and comparisons in Scheme
- _And_: `(and <exp1>...<expn>)`
- _Or_: `(or <exp1>...<expn>)`
- _Not_: `(not <exp>)`
- _Value comparison_: Less than `<`, equal to `=`, greater than `>`

------

## Lecture 12: Input and Output

The form _Read_ will wait for keyboard input and return that input value.

Example:

![Example - Compute-average](/images/scheme-read.PNG)

------

## Lecture 13: Nonfunctional features - I/O

The _Output_ form: `(display <form>)`

Example:

```scm
(display (+ 3 4))  ; this is a non-functional feature; display not does return a value
```

The _Begin_ form: `(begin (form1)...(formn))` starts a sequence of actions (an _imperative_ feature)
