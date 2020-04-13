---
date: "2019-11-04"
category: "Programming"
tags: ['rant', 'programming']
banner: "./photo.png"
image: "./photo.png"
title: "What is programming?"
---

# Preamble
Maybe you've been programming for a while or maybe you just started
programming, after some time you might begin wondering "what IS
programming?". After all, that question ends up being a "what am I
doing?". In this post I'll project my personal view on the matter mixed
with some history, math and some code examples.

# History
To start addressing this question, a historical background must be
provided to understand the relevance and fundamental ideas that have
derived into two main computer programming paradigms, the imperative
paradigm and the functional one.

## Theoretical background
During the 1930s an astonishing breakthrough was done by Alan Turing,
the Turing machine, a universal model of computation. Alongside this
model, another formal definition was done by Alonzo Church, lambda
calculus. Both thesis were proven to be equivalent and serve as a
foundation to today's models of computation.

As of today, lambda calculus is a research topic in the category
theory, a branch of mathematics that studies the relations between
mathematical objects (this will be relevant in a bit). Here are some
related links:
[Category Theory for Computer Science](https://www.math.mcgill.ca/triples/Barr-Wells-ctcs.pdf),
[Computational Category Theory](https://pdfs.semanticscholar.org/3f99/553ca06ce451c5b76479c96e191ad69f3e04.pdf)

## Programmable devices
As electronic circuit projects begun to grow, the complexity of the
projects did so, but exponentially. Thus, taking considerably more
effort to maintain and prove the design correct. Doe to the big costs
that designing and producing specific electronic circuits imply, a more
general solution was developed, the microprocessor. This allowed
developers to reprogram the microprocessor inexpensively, allowing
upgrades, patches and a much faster development process at the expense
of some efficiency.

In order to be programmable, the microprocessors expose a programming
API called Instruction Set Architecture (ISA). In the beginning, all
the development was done in assembly language, an almost direct mapping
to the ISA that adds labels, macros and mnemonics that represent the
instructions. Due to this almost direct mapping, this programming model
presents very limited means of abstraction but permits the expression
of programs in a language that reflects the inner workings of the
processor.

Since computer power was scarce, computer programs needed to be
performant, and in order to achieve this goal, they were written in
assembly. As the computer science field progressed, a need to structure
and organize code emerged, resulting in the creation of programming
languages. 

## Programming languages
Edsger Dijkstra

### Early stages
At IBM, with the release of the IBM 701, the concept of a programming
language was shaped into speedcoding, an interpreted language that
eased expressiveness at the expense of performance. It was meant to
feel like a natural language rather than a machine language. John
Backus submitted a proposal to his IBM superiors to develop a language
that could produce assembly instructions and allowed high performance
numerical computation. This proposal was accepted and resulted in
FORTRAN, a language that has been in use for the past 60 years.

Following the wide adoption of Fortran, other languages started to
appear. Many of them, drew their syntax from Fortran, while others
differed from it. However, there was a fundamental common denominator
among them, they all closely represented a sequence of instructions
based on sequential execution that resembled the processor operational
model.

```fortran
! A fortran fizzbuzz example
PROGRAM fizzbuzz
      IMPLICIT NONE
      INTEGER :: counter 
      
      DO counter=0,100
          IF (MOD(counter,15) == 0) THEN
              WRITE (*,'(A8)') "FizzBuzz"
          ELSE IF (MOD(counter,5) == 0) THEN
              WRITE (*,'(A4)') "Buzz"
          ELSE IF (MOD(counter,3) == 0) THEN
              WRITE (*,'(A4)') "Fizz"
          ELSE 
              WRITE (*,'(I2)') counter
          END IF
      END DO

END PROGRAM fizzbuzz
```

During this era, the 1960s, a lot of the research in the artificial
intelligence shifted towards a different model based on Lisp Machines.
This machines were built upon a lisp interpreter that run on
microprocessors. Thus, "emulating" a computer model on top of a Turing
machine. Lisp itself being based on Church's lambda calculus and
providing a syntax for LISt Processing, is a family of programming
languages that blurs the line that distinguishes data and programs
since it provides a single data structure, the s-expression, to
represent both. This set of features makes it excellent for
metaprogramming and self-modifying code.

It gained a lot of traction shortly after its inception, but not
without having a lot of criticism for having "way to many parens" and
being significantly slower that FORTRAN. Its usage decayed during the
1990s due to the requirements with respect to the early computing
capabilities. Now that computer resources have greatly increased, it
has seen a resurgence in recent years, where the impact of dynamic
typing and garbage collection are negligible in many applications and
the benefits of the pioneered concepts outgrow the computational cost.

Lisp pioneered many computer concepts such as:
 - Higher order functions
 - Garbage collection
 - Dynamic typing
 - Recursion
 - Conditionals
 - REPL

```lisp
;; A lisp fizzbuzz example
(dotimes (run 100) 
    (setq num (+ run 1))
    (write-line (cond 
        ((and (= (mod num 3) 0) (= (mod num 5) 0)) "FizzBuzz")
        ((= (mod num 3) 0) "Fizz")
        ((= (mod num 5) 0) "Buzz")
        (t (write-to-string num)))))
```

During the 70's, after the appearance of Lisp, ML (Meta Language)
started to take shape, this language was envisioned to aid the theorem
prover LCF. Its syntax resembles the one of mathematical functions and
while it permits a functional style, it is still impure and
imperative, however, it makes heavy usage of pattern matching. Also,
its type system includes algebraic data types, type inference,
parametric polymorphism and static typing.

```ocaml
(* A ML (actually OCaml) fizzbuzz example *)
let rec range a b accum =
  if a > b then accum
  else range a (b - 1) (b :: accum)

let fizzbuzz xs = 
  let f = function
    | n when n mod 15 == 0 -> "FizzBuzz"
    | n when n mod 3 == 0  -> "Fizz"
    | n when n mod 5 == 0  -> "Buzz"
    | n -> string_of_int n
  in xs |> List.map f
```

- NOTE: Turing machine \[O(n \log{n})\] or \[O(\log{n})\] added
        complexity when emulating another computing model.
- NOTE: on types with compile time known size and dynamically typed
        languages.
- NOTE: the definition of computable is not well defined. In a
        mathematical sense means that there is a method of obtaining a
        value for a given problem in a deductive manner (somewhat).
- NOTE: on isomorphic grammars.

### From the 80s to the early 2000s
After the success of high level languages in many areas of computing,
there were still people that remained programming in assembly for
performance reasons. Compilers at this time were not able to optimize
as well as they do today. This drove the development of performance
critical software pieces to be written in assembly. With the advent of
operating systems, the codebases that composed the OS started growing
and a need for a language that closely represented the underlying
structure did as well.

Fast forward a couple of years and C started taking shape as it was
being developed alongside UNIX, an operating system that was
architecturally rather simple in response to the complexity of Multics.

The history of Multics and UNIX begun at Bell Labs (now part of AT&T)
and started with Multics, an OS designed to support multiple users at
the same time and preemptive multitasking. As more time, effort and
money were dumped into the project, more and more problems began to
surface. The project didn't scale. In response to a system that tried
to do everything, UNIX was developed by two engineers and they followed
the philosophy "do one thing, but do it well". To aid the development,
the C language was designed and evolved ergonomically with UNIX. The
result was a language that was well structured and has the features
that were needed to create a functional system.

```c
/* A C fizzbuzz example */
#include <stdio.h>

int main(void) {
    for(int i=1; i<=100; ++i) {
        if (i % 3 == 0)
            printf("Fizz");
        if (i % 5 == 0)
            printf("Buzz");
        if ((i % 3 != 0) && (i % 5 != 0))
            printf("number=%d", i);
        printf("\n");
    }

    return 0;
}
```

As C continued with its development, another new player joined in the
landscape of programming languages, a language that tried to unite all
the features that defined functional languages. Its chosen name,
Haskell, in honor to Haskell Curry.

The Haskell 1.0 language definition was released in 1990 after a
meeting at the Functional Programming Languages and Programming
Architecture conference in 1987 that discussed the situation in the
functional community, there were many non-strict purely functional
languages but there was a lack of a common open source language.

Haskell allows to easily express pattern matching, list
comprehensions, lambdas and many other constructs, it also features
lazy evaluation (non-strictness), type polymorphism and behavior
polymorphism through typeclasses. Since it is a purely functional
programming language, its functions do not perform side effects, its
variables are not mutable and almost everything is an expression and
has a type.

This set of features allows programmers to express themselves in a
concise manner and to provide features that can be composed together
in an orthogonal manner, i.e., the primitive concepts are independent
in the sense that they can be learned separately and then easily
pieced together to form a new feature without having to deal with
corner cases.

```haskell
-- A Haskell fizzbuzz example
fizz :: Int -> String
fizz n | n `mod` 15 == 0  = "FizzBuzz"
       | n `mod` 3  == 0  = "Fizz"
       | n `mod` 5  == 0  = "Buzz"
       | otherwise        = show n

main :: IO ()
main = mapM_ putStrLn $ map fizz [1..100]
```

Additionally, during the 90s, c++ gained the relevant features that
make the language stand where it is today. It started in 1982 as a
superset of the c programming language, supporting classes, however,
with time, it started adding many more features.

The most prominent features in c++ are:
 - RAII: a resource management system where variables are created and
   initialized with a constructor and once they go out of scope, their
   destructor is called freeing its corresponding resources.
 - Monomorphisation: in order to avoid overhead in polymorphic (ie,
   generic) containers, functions, etc. they are specialized, reducing
   runtime but increasing binary size.
 - Exceptions: they provide a really useful error handling mechanism,
   however, they interrupt normal control flow.
 - Behavior polymorphism through inheritance.
 - Zero cost abstractions: you only pay for what you use, and what you
   pay for will introduce negligible runtime overhead.

```cpp
#include <iostream>

using namespace std;
int main () {
	for (int i = 1; i <= 100; i++) {
		if ((i % 15) == 0)
		    cout << "FizzBuzz\n";
		else if ((i % 3) == 0)
		    cout << "Fizz\n";
		else if ((i % 5) == 0)
		    cout << "Buzz\n";
		else
		    cout << i << "\n";
	}
	return 0;
}
```

With the dawn of a new millennia Java was created under the lemma of
"Write once, run anywhere" it featured a syntax similar to c++ and was
strictly object oriented. Java boasted its developer friendliness,
productivity, enterprise level and ease of use. This was based on the
fact that the language featured the following properties:
  - Garbage collector
  - Virtual machine with a JIT compiler
  - Byte compilation for portability
  - A huge standard library
  - All the features necessary for object orientation

```java
package start;

import java.lang.System;

public class Main {
  public static void main(String[] args) {
    for (int i=0; i<100; i++) {
      if (i % 15 == 0) {
        System.out.println("FizzBuzz");
      } else if (i % 5 == 0) {
        System.out.println("Buzz");
      } else if (i % 3 == 0) {
        System.out.println("Fizz");
      } else {
        System.out.println(i);
      }
    }
  }
}
```

# What is programming??
If we look up the meaning of programming, a definition like the
following might pop up: "programming is the action of generating a
sequence of instructions for a machine to complete a specific task".
While that is true, it imposes a specific paradigm (the imperative)
where multiple can be used.

When thinking about programming some people describe it as an art,
others as an engineering discipline and some as a science. And, in my
humble opinion, it is a mixture of all of them, it isn't only about
generating a sequence of instructions, when programming, most of the
times, you don't program only for yourself, you also contribute to
others and those others will need to read and understand your code.

# Means of abstraction
