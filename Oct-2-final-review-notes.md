# CSE240 Final Review - October 2, 2022

## TA: Dylan Carey


Agenda
------

1. Final Guidelines
1. C++
1. Scheme
1. Prolog
1. Recursion


Final Guidelines
----------------

The exam will cover **Modules 8 to 13**. There _will_ be a typed question 
for C++. There is **NO** multiple choice for C++ - so you have to 
actually be able to program in C++.

_Breakdown_
- 20% C++, 40% Scheme, 40% Prolog
- ~30 questions in 110 minutes.
- Test is worth 50 points.
- Two types of questions:
  - Multiple Choice (similar to quizzes)
  - Write-in (similar to homework)
- You will **NOT** have the exam released back to you.
- You are allowed _one 3x5 notecard_ (double-sided).
- No scratch paper, writing tools, clean work area, etc.


C++
-----

Remember, C++ is object-oriented programming. It's all about
objects and methods to manipulate data within the objects.

Let's talk about inheritance. We want to make a class structure
like below:

![UML Diagram](/images/uml-cplusplus.PNG)

In order to make this work, we want to have:

```cpp
class Book : public Material() {};
```

If we want to get the _Constructor_ from `Material`:

```cpp
// Generic example without data types
Book(...) : Material(...) {};
// From HW7
Noble(string roomName, int noOfRooms, libraryType libType) : Room(roomName, noOfRooms, libType) {};
```

Now I want to write a new constructor for the `Book` class. Say
I want `title`, `ISBN`, etc.:

```cpp
Book(string title, int ISBN, char[] genre) {
  this->title = title;
  this->ISBN = ISBN;
  this->genre = genre;
};
```

Now let's talk Destructors. If we allocate memory, we should also
clear it up when an object goes out of scope.

```cpp
~Book() {}; // default destructor
```

Technically, in the listed scenario, since we haven't explicitly
allocated memory for anything, `Book` could use `Material`'s 
default destructor and we wouldn't need to explicitly define it.
In the case where there is an explicit allocation, you'd need
to modify the body of the destructor:

```cpp
~Book() {
  delete Author;
};
```

Let's say I have a temporary node `Temp` and a current node, and I 
want to access the name of the author.

```cpp
Temp->next->Author
```

Other reminders:
- Header (`*.h`) files: this is where you declare a class, attributes, and functions (declaration)
- CPP (`*.cpp`) files: this is where you actually create the content for those functions (implementation)


Scheme
------

_Q_: What is the motivation behind functional programming?

_A_: Focuses on _what_ to solve instead of _how_ to do that;
closer to mathematics; higher level of abstraction; no side-effects;
functions are first-class objects (can be put anywhere)

Some main characteristics of _Scheme_:
- No variable types
- No side effects
- Functions are first-class objects (can be put anywhere a value is expected)
- Related to lambda calculus (closer to mathematics)

Explain the following and the syntax to use them:
- `let`: This form is used for scoping variables/values
   ```scm
   (let ((a b)
         (b 5))
	(+ (* a a)(* b b)))
   ```
- `lambda`: This form is used for anonymous functions; one time use; returns a procedure instead of a value
   ```scm
   ((lambda (x y) 
            (* x y))
			3 4)
   ```

_Q_: But why would you use `lambda` instead of `let`?

_A_: A neat example on [StackOverflow](https://stackoverflow.com/questions/2943072/whats-the-point-of-lambda-in-scheme/8546408#8546408)

- _Pairs_: Two "values" together
  ```scm
  > '(1 . 2)
  > (cons 1 2) ; construct the pair
  > (car pair) ; get the first element
  > (cdr pair) ; get the last element (pronounced "cud-der")
  ```
- _Lists_: Nested pairs (except for an empty list, which is NOT of pair-type)
  ```scm
  > (cons 1 (cons 2 (cons 3))) ; makes the list (1 . 2 . 3)
  ; some forms you can use: append, car, cdr
  > (append (list x) y) ; note - list creates a list with parameters as elements
  > (append '(hi dylan) '(in the uk))
  ```

_Q_: What is a higher-order function?

_A_: A function that takes another function as a parameter. _Ex_: `map`, `reduce`, `filter`

- `map`: Applies a procedure to all elements in a list.
   Example: Add 1 to all elements in a list.
- `reduce`: Combine the list into a single result.
   Example: Sum of all items in a list
- `filter`: Filters out element that do not meet a condition/predicate.
   Example: Remove all elements greater than 5

Non-functional features of Scheme:
- `display`, `read`, `begin`

Let's look at some example return values:

```scm
> (append '(1 2 3) '(3 2 1)) ; (1 2 3 3 2 1)
> (car '(8 3 5 4)) ; 8
> (cdr '(7 6 5 4)) ; (6 5 4)
> (cddr '(2 3 4 5 6)) ; (4 5 6)
> (cadr '(4 7 4 2 5)) ; 7
> (caddr '(3 4 7 3 6)) ; 7
> (cdr '()) ; ERROR!!
```


Prolog
------

_Q_: What is the main idea of _Prolog_?

_A_: Specify what is needed in the form of facts and queries instead
of how it is done (abolish all programming).

_Q_: How do we pass an integer out of a rule?

_A_: Let's say you have a rule called `my_rule(A, B, C)`. To get a value back, you'd want to call it with using a variable:

```
/* Sorry - no prolog Markdown syntax highlighting :( */
?- my_rule(1, B, 2).

B = whatever
```

An anonymous variable in Prolog is a placeholder: `_` ; it can be anything; a free variable.

_Q_: What does it mean when a question and a fact unify?

_A_: Same predicates, same arity (# of parameters), and identical arguments.

_Q_: When a question matches a rule, in what order does the 
unification take place? (What matches first, second, etc.?)

_A_: This is easier explained through a graphic:

![Example - grandmother rule](/images/prolog-order.PNG)

So basically, it checks:
1. Facts
1. Rule
   1. Facts in rule - makes sure they match

Output examples:
```
/* CAREFUL! This is looking for the member that is a list of just "cat" */
?- member([cat], [dog, cat, mouse]).

no 

/* NOTE: You will get the X and Y values out */
?- member(X, [81, 25, 9, 69]), Y is X * X, Y<400.

X = 9
Y = 81 ;
true / yes
```

Let's identify / define the following:

```
somePred(X, [x]).
somePred(X, [_ | Tail]) :- somePred(X, Tail).
```

What does this do? _Returns the **LAST** element!_

Another one:

```
anotherPred(X, [X | _]).
anotherPred(X, [_ | T) :- anotherPred(X, T).
```

What does this one do? _Check if `X` is in a list._

That is: `?- anotherPred(5, [1 2 3]). <- false`

And yet _another_ one:

```
aPred([], []).
aPred([X | L}, F) :- aPred(L, G), append(G, [X], F).
```

What does this one do? _Reverses a list._

Switching gears... What is the output?
```
foo(X, Y) :- Y is 5*X; X is Y/5.

?- foo(X, 10).
/* This gives an error: because it's a logical flaw. */
```


Recursion
---------

_Q_: What aspect of recursion leads to slow performance?

_A_: Deferring function calls; adding calls onto the stack; 
putting off work until later.

_Q_: How can we make a more iterative recursive procedure in Scheme?

_A_: Adding parameters to the recursive call to mimic state 
variables in a loop (e.g., a counter); use tail recursion.

_Q_: Why can we use iteration and recursion to solve both 
factorial and Fibonacci sequence problems?

_A_: There is no one algorithm to solve these problems. You could 
do them a lot of ways. Problems like Towers of Hanoi, though, 
would be much more difficult iteratively than recursively.


Closing
-------

**REMEMBER** to take note of these concepts:

- (C++) Study how to implement classes, inheritance, polymorphism, constructors, and destructors.
- (Scheme) How using higher-order functions made mergesort generic and not limited to numbers only.
   - Parameters were added to the algorithm to specify specific procedures for examining data.
- (Scheme) Purposes for being able to return a procedure from a procedure
   - It can be used to create another procedure that is bundled with some information.
- (Scheme) Practice writing procedures without an IDE
   - E.g., convert a piecewise function into a procedure
- (Prolog) What is improper about circular definition of a rule?
   - Improper use of recursion
- (Prolog) Be quite familiar with quicksort in Prolog and how to choose different pivot elements
- Practice code tracing in Scheme and Prolog.
