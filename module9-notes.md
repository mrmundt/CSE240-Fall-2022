# Functional Programming (Scheme) II
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

------

## Lecture 1: Let-Form and Unnamed Procedures

_Definitions_

> **Environment**: List of names and corresponding values that are valid ("known") during and after
>                  the execution of a program.

In Scheme, everything is defaulted to _global_ scoping. You can change this using _Let_.

_Syntax_:

```scm
(let ( (name1 val1)
       ...
       (namen val n))
 body)
```

The scope is only within the `body` of the procedure. The `body`
will return a value at the end which is the evaluation of any expression.

------

## Lecture 2: An Example of Scoping

Let's assume we want to build a space habitat. What volume of material do we need?

![Example - space habitat](/images/space-habitat.PNG)

```scm
(define (habitat-material height radius thickness)
  (let ((PI 3.14159265))
    (let ((cylinder (lambda (r h)
      (* h (* PI (* r r))))))
    (- (cylinder radius height)
       (cylinder (- radius thickness)
                 (- height (* 2 thickness)))))))
```

In this example, `PI` and `cylinder` cannot be accessed outside of `habitat-material`.

------

## Lecture 3: Example - ABS and ASR

This was a more involved example; better to watch this one.

------

## Lecture 4: Applying Arguments

New form _Lambda_: `(lambda (<parameters>) <body>)`

The value returned from `lambda` is a procedure rather than a basic data type.

Example:

```scm
((lambda (x y) (+ (* x x) (* y y))) 3 4)  ; results in 25
```

Another example:

```scm
((lambda (x y) (+ (* x x) (* y y)))
  3
  ((lambda (z) (+ z 3)) 4))  ; results in 58
```

------

## Lecture 5: Conversion

You can convert between `let` and `lambda`!

_Let-form_:

```scm
(let ((x 9))
  (let ((x 3)
        (y (* 5 x)))
  (+ x y)))
```

_Lambda form_:

```scm
((lambda (x y)
  ((lambda (x y)
    (+ x y))
    3 (* 5 x)))
    9)
```

------

## Lecture 6: Structured Data

_Definitions_

> **Pair**: A fundamental data type; pair of elements `(x . y)`

Operations
1. _Constructor_: `(cons a b)` makes `(a . b)`
2. _Accessors_: `(car pair)` gives the first value; `(cdr pair)` gives the second value (pronounded "cud-der")
3. _Predicate_: `(pair? x)` returns true or false

Pairs can be used for... (examples)
- The position of a city `(latitude . longitude)`
- Collections of data

------

## Lecture 7: Dot and Box Notation

When you have a nested list of pairs, it can look messy. The simplification rule:
omit the dot and the parentheses when the item to the right of the dot is a pair.

Example:

```scm
(1.(2.(3.4)) ; this becomes (1 2 3 . 4)
```

Box notation is another way to represent pairs.

![Box notation for pairs](/images/scheme-box.PNG)

Box and Arrow (Tree) is a third way.

![Box and arrow/tree notation](/images/scheme-box-arrow.PNG)

------

## Lecture 8: Quotes and Symbols

Pairs in scheme neec the symbol tick: `'(1 . 2)` because everything in parentheses is an application to be evaluated.

What can/must be quoted?
- **MUST** quote pairs and lists
- **MUST NOT** quote sub-lists
- **MUST-NOT** quote forms to be evaluated
- _May_ quote numbers, strings, and booleans - but it makes no difference so just don't

_Symbol_ operations
- _Constructors_: through input; anything you enter is a symbol (e.g., `12we1`)
- _Accessors_: `symbol->string`
- _Predicates_: `(symbol? x)` returns true/false; `(eq? x y)` returns true of `x` and `y` are equal

------

## Lecture 9: Lists

There are two definitions for a _List_:

```scm
<list> ::= `()             ; empty list - NOT a pair
<list> ::= (cons x <list>) ; x is any Scheme form
```

Besides the first case, every list is a pair.

Operations
- _Constructors_: `(cons x a)`, `(list item1 ... itemn)`, `(append list1 list2)`
- _Accessors_: `(car anylist)`, `(cdr anylist)`, `(length anylist)`, `(list-ref list position)`, `(list-tail list position)`
- _Predicates_: `(list? x)` returns true if `x` is a list

------

## Lecture 10: Comparing Pairs and Lists

List-type and pair-type are **NOT** equivalent.

- Both are constructured by `(cons a b)`
- Some operations produce the same results; some do not
- Pair-type is **NOT** a sub-type of list-type. However...
- List-type is a sub-type of pair-type, EXCEPT for an empty list `'()`

------

**NOTE**: The last lecture is all examples of list usage. Better to watch this one.

