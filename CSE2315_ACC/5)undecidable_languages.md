# Undecidable languages

---

Reduction: using another algorithm as a part of another algorithm to prove a problem is (un)decidable.
- DR: Direct reductions
- MR: Mapping Reductions


## DR - The Universal Turing Machine
> The Universal Turing Machine is a recogniser (but not a decider) for the acceptance problem.

Recall the acceptance problem:<br>
The language A = {<M,w> | M is a TM and M accepts w} is Turing recognisable.
- Note that this problem is not decidable
- We can run M on w. If it halts and accepts, accept. If it halts and rejects or loops, reject.

## DR - Non-Turing Recognisability
### Infinity
Let's start with some set terminologies:
- One-to-one (injective): if a != b then f(a) != f(b)
- Onto (surjective): every element in the range is "hit"
- Correspondence (bijective): one-to-one and onto 
  - Two sets have the same size iff there exists a correspondence between them.


- Countable: a set is countable iff it has a finite size, or there is a correspondence with N = {1, 2, 3, ...}
  - Countably infinite: when a set is infinite but is countable


Countably infinite - example proofs:
1. The set of odd numbers is countably infinite
   - X = the set of odd numbers, Y = N
   - Let f = 2x - 1.
   - X has a correspondence with Y
   - X is also a subset of Y
   - Therefore, the set of odd numbers is countably infinite
2. The set of rational numbers is countably infinite
   - R = {M/N | M,N ε N}
   - List all the rational numbers in a table
     - ```
             1    2    3    4    5  ...
         1  1/1  1/2  1/3  1/4  1/5
         2  2/1  2/2  2/3  2/4  2/5
         3  3/1  3/2  3/3  3/4  3/5
         4  4/1  4/2  4/3  4/4  4/5
         5  5/1  5/2  5/3  5/4  5/5
       ...
       ```
     - We can then print the rational numbers (diagonally) to enumerate them (this is called the ***diagonalisation method***)
     - This creates a correspondence with N
     - Therefore, ...
3. The set of irrational numbers is uncountably infinite
   - X = the set of irrational numbers
   - X = {n | n has an infinite decimal expansion}
   - Assume that X is countably infinite
   - Then we can put it in a correspondence (make the table and list (enumerate) them in order)
   - Say w = the number created by taking the diagonal of the table.
   - If we increment 1 for add the digits in w, we get a new number that is not on the table
   - Creates a contradiction, therefore ...

### Languages that are not Turing Recognisable
> The set of all Turing Machines is countably infinite<br>
> i.e., We can enumerate the set of all Turing Machines

Approach 1:
- Every TM can be encoded into a string (of 0's and 1's of finite length)
- Every string is either a valid TM representation or not
- Generate all strings, one after the other
- Check to see if it is a valid representation of TM

Approach 2:
- The alphabets are finite. There are a finite number of kinds of transitions (in the form a -> b, R)
- For i = 1,2,3,...
  - There is a finite number of directed graphs with i nodes
  - There is a finite number of ways to label the edges
  - Generate them all
- End

> The set of all infinite length strings over {0,1} is uncountably infinite

Proof (by diagonalisation method):
- Recall the irrational numbers problem
- Assume the set of infinite binary strings can be enumerated
- Then we can put it in a correspondence using the table
- Take the diagonal and flip the bits. Now this string is a new string that is not in the table
- This creates a contradiction...

> The number of all languages is uncountably infinite

- The set of all finite length strings over Σ = {a,b} is countable
- A language contains some of those strings and not others. i.e., A language is a subset of an infinitely countable set.
- This means that a language can be fully specified by giving an infinite length binary string
  - if the nth digit of the string is 1, then the language contains the nth word in the set
- There are uncountably many infinite length binary string
- Therefore the number of all languages is uncountably infinite

<br>

This means that some languages are not Turing Recognisable
- The number all TM's are countably infinite
- = The number of all Turing Recognisable languages is infinite
- But the number of all languages is uncountably infinite
- Therefore there exists languages that are not Turing Recognisable


## MR: Undecidability of the Halting Problem
> The language A = {<M,w> | M is a TM and M accepts w} is undecidable.

Proof:
- Assume A is decidable
- Let H be the algorithm/TM that decides A.
  - H(<M,w>) = 
    - Accept if M accepts w
    - Reject if M does not accept w
- Using H, construct a new machine D:
  - Input to D: <M\> = the description of a TM, M
  - Action:
    - Run H as a subroutine
    - Ask whether machine M would accept if given a description of itself as input (H(<M, description of M>))
  - Output: if H accepts, then reject. If H rejects, then accept.
- Run D on itself:
  - D(<D\>) = Accept if D rejects <D\>. Reject if D accepts <D\>.
  - This is a paradox:
    - H accepts <M,w> exactly when M accepts w.
    - D rejects <D\> exactly when M accepts <M\>.
    - D rejects <D\> exactly when D accepts <D\>.
- Contradiction, ...

## MR: Undecidability of the complement of the Halting Problem
### Not Turing-Recognisable Languages
> If a language L is decidable, then L is Turing Recognisable and its complement L- is Turing Recognisable
- Every decidable language is Turing recognisable
- Want to recognise L-? Just run the decider for L and give the opposite answer.

<br>

> If a language L is Turing recognisable and its complement L- is also Turing recognisable, then L is decidable.

Want to decide L? (Is x in L?)
- Let M1 be the recogniser for L
- Let M2 be the recogniser for L-
- Run M1 and M2 in parallel
- x is in either L or L-. Either M1 or M2 (or both) will eventually halt and one of them will accept.
- If M1 accepts, then accept. If M2 accepts, then reject.

<br>
Now put these together to get...

> A language L is Turing recognisable iff it is Turing recognisable and co-Turing recognisable

A language is "co-Turing recognisable" if its complement is Turing recognisable


Recall that the acceptance problem for a Turing Machine is Turing recognisable but not decidable.<br>
With the logic above, we can conclude that the complement of the acceptance (halting) problem for a TM is not Turing recognisable.


## DR: More direct reductions
### Reducibility
A technique for proving undecidability

Reduce a hard problem onto an easier problem.
The reverse of this is if the hard problem is unsolvable, the easier problem is unsolvable too.

Example: Prove that a problem P is undecidable.
- Assume P is decidable
- Reduce A_TM (a "hard" problem) into P (the "easier" problem)
- Use the solution of P to solve A_TM
  - Use the decidability of P to find an algorithm to decide A_TM
  - Build a TM to decide A_TM using the TM to decide P as a subroutine
- But we know that a decider for A_TM cannot exist
- Contradiction, therefore P is not decidable

### The Halting Problem: Proof of Undecidability
"Does a program halt when give a specific input?"

The language HALT_TM {<M,w> | M is a TM and M halts on input w} is undecidable.
- Assume it is decidable (i.e., there is a TM R that decides HALT_TM)
- Use R to build another TM S that decides A_TM (reduce A_TM to HALT_TM)
  - A_TM
    - A_TM = {<M,w> | M is a TM that accepts w}
    - To decide A_TM, S:
      - Given M and some input w,
      - If M accepts w, then accept
      - If M rejects w or loops, then reject
    - Deciders never loop.
  - R
    - R = A TM that decides HALT_TM = {<M,w> | M is a TM that halts on w}
    - To decide HALT_TM, R:
      - Given M and some input w,
      - If M accepts or rejects w, then accept
      - If M loops on w, then reject
  - Goal: construct S, a decider for A_TM
    - Input: <M,w>
    - Run R on <M,w> to see if M halts or loops. R is a decider, so R will never loop.
    - If R rejects, it means M loops. Then reject.
    - If R accepts, it means M halts.
    - Simulate M on input w. When M halts,
      - If M accepts, then accept
      - If M rejects, then reject
  - So S is a decider for A_TM
- But A_TM is undecidable
- Contradiction

### The Emptiness Problem
"Does a TM accept any string?"
an
The language E_TM = {<M\> | M is a TM and L(M) != ∅} is undecidable.
- Assume that R decides E_TM
- Use it to construct S, a decider for A_TM
  - Goal: construct an algorithm S which is given <M,w> and decides whether M accepts w
    - Step 1: construct M'
      - Algorithm for M':
        - Input: x
        - If x != w then reject.
        - Otherwise, simulate M on x. If M accepts then accept, d if it rejects then reject.
      - Note:
        - L(M') = {w} if M accepts w
        - L(M') = ∅ otherwise
    - Step 2: use R to decide whether L(M') is empty or not
      - R accepts => L(M') = ∅ => M does not accept w
      - R rejects => L(M') = {w} => M accepts w
- But A_TM is undecidable. So contradiction

## MR: Mapping Reductions
### Reducing One Language to Another
> Language A reduces to language B <br>
> if there exists a computable function f: Σ* -> Σ*<br>
> such that, for every x, x ε A iff f(x) ε B

So far we used: If A reduces to B and A is undecidable, then B is undecidable.<br>
We can also use: If A reduces to B and B is decidable, then A is decidable.<br>
We can also change decidable to Turing recognisable.