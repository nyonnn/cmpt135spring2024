[[O-notation]] is a useful way to classify algorithms according to their running-time. For example, here are 7 common classifications of algorithm performance:

| O-expression  | Name         | Example                   |
|---------------|--------------|---------------------------|
| $O(1)$        | constant     | $1, 10, 34, 3538, \ldots$ |
| $O(\log n)$   | logarithmic  | $8\,\log_2 n + 5$         |
| $O(n)$        | linear       | $29n+5, n-9000$           |
| $O(n \log n)$ | linearithmic | $n\,\log_3 n + 23n - 4$   |
| $O(n^2)$      | quadratic    | $7n^2 - 4n + 22$          |
| $O(n^3)$      | cubic        | $n^3 + 2n^2 + 22n + 1$    |
| $O(2^n)$      | exponential  | $3^n + n^4 - 2n^2 + 80$   |

There is another classification that is of interest in theoretical computer science: **exponential running time or worse**, versus **less than exponential running time**. If a problem can only be solved by an algorithm whose worst-case running time order is exponential (or worse), we will call that problem **hard**. Problems that can be solved in better than exponential worst-case running time we'll call **easy** problems.

For example, problems like [[basic sorting|sorting]], [[linear search]], [[binary search]], and finding the min of an array can all be solved in time $O(p(n))$ where $p(n)$ is a *polynomial* in $n$. So they are all *easy* problems.

But some problems are hard, meaning that the best algorithms for solving them may take exponential, or worse, time. For example:

- generating all bit-strings of length $n$ takes time proportional to $O(2^n)$, because there are $2^n$ bit strings of length $n$
- generating all permutations (i.e. arrangements) of $n$ different numbers takes time proportional to $O(n!)$, because $n$ different numbers can be arranged in exactly $n!=1 \cdot 2 \cdot 3 \cdot \ldots \cdot n$ ways.

> **Permutation sort** One *very* slow way to sort a vector is to generate all permutations of its elements, one at a time, stopping when the elements are all in sorted order. This requires checking $O(n!)$ different permutations in the worst case. 

Interestingly, there is a large group of important and useful problems that no one knows yet whether they are easy or hard. One of those problems is the **Traveling Salesman Problem**.
## The Traveling Salesman Problem

**The Traveling Salesman Problem (TSP)** is a famous computational problem that is easy to state and also has many applications.

Given a list of cities positioned on a map (so you know the distance between any two cities), what is the *shortest* (in terms of total length) tour that visits all the cities, starting and ending at the same city?

For example, here is a map of the USA where the red dots are the capital city of each state:

![[Pasted image 20240404191621.png]]

The blue line shows a shortest possible tour that visits all the states.

In general, suppose you have a map with cities  named $c_1, c_2, \ldots, c_n$. If you start at $c_1$, then you might visit $c_4$ next, and then maybe $c_2$, and so on. Eventually you come back to $c_1$.

Each arrangement of $c_1, c_2, \ldots, c_n$ corresponds to a different tour, and the TSP asks which of these tours has the *shortest* total length.

The "obvious" brute-force solution generates all possible tours and then chooses the shortest. But there are $O(n!)$ tours, so a brute-force algorithm would have to examine (more than!) an exponential number of tours.

The TSP is a well-studied problem, and there are algorithms that can solve particular instances more efficiently than brute-force. But, so far, no one has discovered an algorithm that can solve *every* TSP instance in polynomial time (or better). In other words, it is unknown if the TSP is an easy or hard problem.

Since it has not been proven that a polynomial time algorithm *doesn't* exist for solving the TSP, there is the possibility that one day someone (maybe you!) could find such an algorithm. But beware: most computer scientists believe that no such algorithm exists, and that the best that can be done are either approximation algorithms that can get *close* to the best solution (but can't guarantee it's the best), or algorithms that are efficient only in certain special cases.

> **Note** The TSP has a rich history. This [TSP Website](http://www.math.uwaterloo.ca/tsp/) discusses the problem in depth, and has many interesting examples, including lists of the best-known TSP tours for various maps

## NP-Completeness
The TSP is a member of a set of algorithmic problems known as [[NP-complete problem|NP-complete problems]]. Here are a couple of other [[NP-complete problem|NP-complete problems]].

## [Logical satisfiability (SAT)](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem)
Given a logical expression such as "((not p) or (not q)) and r", find true/false values for p, q, and r that make the expression true (i.e. that *satisfy* it). It is not hard to imagine an algorithm that tries all possible true/false values for the expression to see which, if any, make it true. But that brute-force approach doesn't work well in practice because you can easily run into expressions with *hundreds* or even *thousands* of variables, and trying all true/false values for all $n$ variables takes $O(2^n)$ time.

There are efficient *practical* algorithms, called [SAT solvers](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem#Algorithms_for_solving_SAT>), that can quickly satisfy many large logical expressions. This turns out to be quite useful in applications such as scheduling.

But there is no known SAT-solving algorithm that runs in less than exponential time for *all* logical expressions. All known general-purpose SAT algorithms run in $O(2^n)$ (or worse!) in the worst case.

## [The Number Partition Problem](https://en.wikipedia.org/wiki/Partition_problem)
Given a set of $n$ integers, can you arrange them into two groups such that the sum of the numbers in each group is the same (or as close as possible)?

For example, suppose you and a friend are carrying a bunch of grocery bags from shopping. How can you divide the bags between yourselves so that you each carry the same weight (or as close as possible to the same weight)?

Like SAT, efficient algorithms are known for solving *some* instances of this problem, but in general there is no known algorithm that always runs in less than exponential time for *all* instances. But no one has proven that such an algorithm doesn't exist.

## NP-Complete Problems
[[NP-complete problem|NP-complete problems]] are a subset of hard problems that have an amazing property: if any *one* NP-complete program is easy, then *all* NP-complete problems are easy. In other words, if you can find a worst-case polynomial time algorithm for *any one* NP-complete problem, then there must be worst-case polynomial-time algorithms for *all* NP-complete problems.

Currently, no one knows if *any* NP-complete problem has a polynomial-time worse-case solution.

Most computer scientists believe that *no* NP-complete problem is easy. There are hundreds of NP-complete problems ([take a look at the list given here](https://en.wikipedia.org/wiki/List_of_NP-complete_problems)), many of them well-studied for decades, and it seems unlikely that they could *all* be easy.
 
However, no one has been able to *prove* that NP-complete problems are not easy. Many computer scientists consider this to be the most important unsolved problem in all of theoretical computer science. It is often referred to as the **P=NP problem**.

## Undecidable Problems
We know that NP-complete problems can be solved, we just don't know how efficiently in the worst case. But there are computational problems for which it has been proved that no algorithm at all *exists* for solving them! Such problems are called **undecidable problems**.

For example, suppose you want to write an **infinite-loop checker**. This is a program that takes the source code of another program as input, and returns "yes" if there's an input for the input program that causes it to go into an [[infinite loop]], and "no" otherwise. Such a program could be useful for debugging programs.

It turns out that there is no such a program. It's not just that it would be *hard* to write, or that such a program would run very inefficiently --- such a program *does not exist*.

> [Here is a good short video](https://www.youtube.com/watch?v=92WHN-pAFCs) that demonstrates the essential idea of why an infinite-loop checking program doesn't exist.

This particular example of undecidability is known as [the halting problem](https://en.wikipedia.org/wiki/Halting_problem), and it was first solved in 1936 by the mathematician [Alan Turing](https://en.wikipedia.org/wiki/Alan_Turing):

![[Alan_Turing.png]]

As part of his proof, he also developed the notion of what are now called [Turing Machines](https://en.wikipedia.org/wiki/Turing_machine). To this day they are still one of the standard theoretical models of computation.

> In addition, Turing is often considered to be a founding father of artificial intelligence, due to his early work on chess-playing and his description of the famous [Turing test](https://en.wikipedia.org/wiki/Turing_test).

For more examples of undecidable problems, [check out this list](https://en.wikipedia.org/wiki/List_of_undecidable_problems).
## Practice Questions
1. What does it mean if an [[algorithm]] runs in polynomial-time?
2. Given an example of a computational problem that cannot be solved in polynomial-time.
3. What do mean when we say a computational problem is *easy*, or *hard*?
4. Suppose an instance of the traveling salesman problem has 25 cities. If you solved it using brute force, about how many different tours would you need to check?
5. What does it mean for a problem to be NP-complete? Give an example of an NP-complete problem.
6. What does it mean if a computational problem is undecidable? Give an example of an undecidable problem.
7. Pete the programmer thinks that it *is* possible to write an [[infinite loop]] checker in C++. "All you need to do," says Pete, "is search for patterns of infinite loops, like for(;;) { ... }, or while(true) { ... }. Sure, there would be a bunch of such patterns, but if you had the time you could write a program that checks for them all."  Why does Pete's approach *not* solve the halting problem?
