# Imperative Programming (C & C++) IIII
### ASU CSE 240, Fall 2022
### Instructors: Bansal, Acuna

------

## Lecture 1: Recursive Problem Solving

_Definitions_

> **Recursion**: a technique that solves a problem by solving a smaller problem of the same type

----

Let's consider computing the factorial of a number `n`:

```c
int Factorial(int n) {
  if (n == 0) return 1;
  else return n*Factorial(n-1);
}
```

Why should we use it?
- Produces elegant, easily understandable code
- Can sometimes be the easiest way
- Usually solves a more general version of the problem

------

## Lecture 2: General Structure

_Definitions_

> **Recursive Function**: A function is recursive if it calls itself within the function.
> 
> **Tail-recursion**: A structure which calls itself only once and in the last statement. (Similar to a do-while loop)

The rest of this lecture was examples.

------

## Lecture 3: Recursive Formulation

The Four Step Approach:

1. Formulate the size-n problem
2. Find the stopping condition(s) and the corresponding return value(s)
3. Formulate the size-m (m < n) problem and find m. (normally, m = n-1)
4. Construct the size-n solution from the size-m problem

Example: Insertion sorting

1. `int *sorting(int *a, int n)`
2. What is the smallest array? ... One element! And we should just return that back.
3. Assume array of size `n-1` is sorted and we need to add a new element.
4. We need to insert the new element into the list at the correct spot.
   _NOTE_: **THIS** is the actual computation step.

------

**NOTE**: Lecture 4 shows example of how to do the Tower of Hanoi and fractal problems.

------

## Lecture 5: Binary Search Trees (BST)

_Definitions_

> **Linked List**: each node has ONE next node
> 
> **Graph**: each node is allowed more than one next node
> 
> **Tree**: does not contain a loop; no more than one path between any two nodes
> 
> **Height/Depth of a Tree**: number of edges from the root of the tree to the furthest leaf
> 
> **Binary Tree**: any of the nodes can have at MOST two next nodes
> 
> **Full Binary Tree**: each node has 0 or 2 child nodes
> 
> **Balanced Binary Tree**: heights of any two leaf nodes never differ by more than one
> 
> **Binary Search Tree**: left branch has smaller values, right branch has larger values

------

Data structure for BST:

```c
struct treeNode {
  int data;                       // key
  struct treeNode *left, *right;  // pointers
}
```

Traversal options:
- _Preorder_: root, left, right
- _Inorder_: left, root, right (should print in numerical order)
- _Postorder_: left, right, root

Balancing a tree improves search speed, as does allowing more children. Complexity summary:

![BST Search Complexity](/images/bst-complexity.PNG)

-----

## Lecture 6: BST Implementation

_NOTE_: This lecture has a lot of examples with pictures. I only provide the recursive approach.

Traversing via recursion:

1. Formulate the size-n problem. (No return value needed.) `void traverse(struct treeNote *top)`
2. Find the stopping condition and the corresponding return value. `if (p == NULL) and return NULL;`
3. Formulate the size-m problem and find m. In many cases, m = n - 1; `traverse(p->left); then traverse(p->right);`
4. Construct the solution of size-n problem from size-m problem.
   
   ```c
   traverse(p->left);
   printf("data = %d\n", p->data);
   traverse(p->right);
   ```

Full solution:
```c
void traverse(struct treeNode *top) {
  struct treeNode *p = top;
  if (p != NULL) {
    traverse(p->left);
    printf("data = %d\n", p->data);
    traverse(p->right);
  }
}
```
