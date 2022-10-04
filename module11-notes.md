# Logical Programming (Prolog) I
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

------

## Lecture 1: The Logic Paradigm

_Definitions_

> **Logic Paradigm**: The focus is on _what_ is needed (requirements) instead of _how_.
> We rely on the environment to find solutions that meet requirements.
> 
> **Fact**: What is known in the environment. `fast(car).`
> 
> **Rule**: What can be inferred from facts. `father(bill, joe) :- son(joe, bill).`

The _Logic Paradigm_ is different from the previous paradigms for several reasons:

1. Takes a step further to fully abolish programming altogether. Rather
   we describe the environment and let the computer find a way to solve it.
1. Easily convey logic-based ideas into written form.
1. Prolog uses a simplified variation of predicate logic symbols.

------

## Lecture 2: Prolog Basics

_Definitions_

> **Fact**: Also called _axioms_; absolute truths about objects and their relationship.
> 
> **Rule**: extend facts about and between objects; conditional truths.
> 
> **Queries**: questions; goals; request information about objects and relationships. `?- grandmother_of(jane, calvin).`
> 
> **Arity**: number of arguments.

_Goals, Queries, or Asking Questions_

A goal succeeds if there are fact and/or rules that match or _unify_ the goal:
1. Predicates are the same
2. Arity is the same
3. Corresponding arguments are identical

_Variables_

More complex questions are possible with the use of variables. For example:

```
?- pred(X1, ..., XN).  /* NOTE: Variables in Prolog _MUST_ start with uppercase letter */
```

There are also _anonymous variables_ which basically represent free variables ("don't care, match everything"):

```
?- weather(City, _, hot).
```

_Compound Queries_

You can force a matching of multiple queries using _AND_ `,` and _OR_ `;`.

```
?- weather(C, summer, hot), weather(C, fall, hot). /* Find cities where it is hot in both summer and fall */
```

------

## Lecture 3: Rules

_Definitions_

> **Rule**: states a general relationship, normally using variables as arguments, that may
> be used to conclude a specific fact or another rule.
> 
> **Structure**: represent nested relationships

_Syntax_: `relationship(obj, ..., obj) :- relationship(obj, ..., obj).` <- head/conclusion, neck/if, body/condition.

Example:

```
grandmother(X, Y) :-
  mother(X, Z),
  parent(Z, Y).
```

This brings up the concept of scope. The scope of a Prolog variable is only within the fact, rule,
or query that contains it.

------

## Lecture 4: Searching for a Solution

This lecture talks about how Prolog searches for a solution. This is best explained
via the graphic on slide 27:

![Prolog resolve order](/images/prolog-order.PNG)

------

## Lecture 5: Operators

Prolog has a weakness in expressing numeric computation. So it provides shorthand options.

_NOTE_: The following list is not exhaustive.

1. item1 @>= item2 (not restrictive to numbers)
2. item1 @< item2  (not restrictive to numbers)
3. X == 'Zooey'.
4. Y \== 'Zooey'.
5. 12 =:= 25.
6. 12 =\= 24.
7. 0.5 =< 4.

There is also a generic form for arithmetic operators: `<var> is <arith_exp>`

```
?- X is 1+3.
```

------

## Lecture 5: Recursion Basics

A _rule_ is recursive if a class in the condition matches the conclusion: they have the same predicate and arity.

The example given in this lecture was finding an ancestor in a factbase:

```
/* Stopping condition - goes first */
ancestor(A, D) :-
  parent(A, D).

/* Size-n problem */
ancestor(A, D) :-
  parent(A, P),
  ancestor(P, D). /* Size n-1 */
```
