# Functional Programming (Scheme) III
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

------

## Lecture 1: The Factorial Process

A factorial is a well-formed problem for a recursive solution. The solution can be written:

```scm
(define (factorial n)
  (if (= n 1)
      1
      (* n (factorial (- n 1)))))
```

Each call adds to the stack:

```scm
(factorial 6)
(* 6 (factorial 5))                           ; start adding calls to the stack
(* 6 (* 5 (factorial 4)))
(* 6 (* 5 (* 4 (factorial 3))))
(* 6 (* 5 (* 4 (* 3 (factorial 2)))))
(* 6 (* 5 (* 4 (* 3 (* 2 (factorial 1))))))   ; finally reached the base case - now we can actually evaluate
(* 6 (* 5 (* 4 (* 3 (* 2 1)))))
(* 6 (* 5 (* 4 (* 3 2))))
(* 6 (* 5 (* 4 6)))
(* 6 (* 5 24))
(* 6 120)
720                                           ; final result!
```

Man. That was a lot of calls added to the stack. All of the calculations needed
to be deferred. But... We can also solve this using iteration.

Iteration? That's imperative! "An
iterative process is one whose state can be summarized by a fixed number of
state variables" (SICP).

But we _can_ do this in Scheme if we set up a counter...

------

## Lecture 2: Iterative Factorial

```scm
(define (factorial n)
  (fact-iter 1 1 n))

(define (fact-iter product counter max-count)
  (if (> counter max-count)
      product
      (fact-iter (* counter product)
                 (+ counter 1)
                 max-count)))
```
This time, there is no pushing on the stack. So what's the moral of the story?

Recursion can _sometimes_ cause problems:
1. Need to allocate stack memory for every call
2. Too many recursive calls gives a stack overflow

------

## Lectures 3-6: Recursion Examples

This set of lectures is better to watch. Many of the examples became relevant in the homework.

------

## Lecture 7: Higher-Order Functions Introduction

_Definitions_

> **Higher-Order Function**: A function that takes another function as an argument or returns one.

In Scheme, there are three classic example of higher-order functions:

1. _Mapping_: applying the same procedure or operation to all elements in a list
2. _Reduction_: take many elements of a list to compute one result
3. _Filtering_: remove elements that do not satisfy a predicate

------

## Lecture 8: Mapping

_Syntax_: `(map proc list)` - applies the procedure `proc` to all items of `list`

Example:

```scm
(define (foo x) (...))
(map foo '(3 6 9 12))

(define (not-gate x) (if (= x 0) 1 0))
(map not-gate list)
```

An example implementation of `map`:

```scm
(define map1
  (lambda (proc a-list)
    (if (null? a-list)
        '()
        (cons (proc (car a-list))
              (map proc (cdr a-list))))))
```

------

## Lecture 9: Reduce

_Reduce_ allows us to combine multiple results from a map into a single result.

Example: `sum-list` - sum all elements in a list

```scm
(define sum-list (lambda (x)
  (if null? x)
            0
            (+ (car x) (sum-list (cdr x))))))
```

Reduction provides a generic way to handle all these functions by
constructing a value that depends upon all members of a list.
Like mapping and filtering, the idea is to apply a reduce function to
another function.

An example implementation:

```scm
(define reduce
  (lambda (op base x)
    (if (null? x)
         base
         (op (car x) (reduce op case (cdr x))))))
```

------

## Lecture 10: Filter

_Filter_ is similar to mapping in that a procedure is applied to all members of a list.

_Syntax_: `(filter proc list)` <- but `proc` here is actually a predicate. All elements that
do not meet the predicate will be removed from the list.

Example:

```scm
(filter (lambda (x) (> x 200)) '(50 300 65 800)
```

An example implementation:

```scm
(define filter (lambda (pred list)
  (if (null? list)
      '()
      (if (pred (car list))
          (cons (car list) (filter pred (cdr list)))
          (filter pred (cdr list))))))
```

------

## Lecture 11: Procedures as Return Values

Because Scheme supports higher-order programming, a procedure can be used anywhere a variable might.

A common use case: have a procedure that builds another type of procedure and bundle them together.

Example:

```scm
; a proc that builds an incrementor
(define (inc-maker inc)
  (lambda (x) (+ x inc)))

; two incrementor procedures
(define inc5 (inc-maker 5))
(define inc10 (inc-maker 10))

> (inc5 100)
105
```

## Lecture 12: Generic Algorithms

One of the example videos (Lecture 6) shows how to do mergesort. But that solution breaks
down as soon as we introduce non-numbers to our list.

This can be resolved by using higher-order functions.

(From here, it's better to watch the video.)
