# Decidable Languages

---

# Enumerators
An enumerator produces a sequence of strings (generates/enumerates language)

An enumerator is like a TM:
- It has an infinite tape and a finite state control
- But it also has a "printer"

Operations:
- The tape is initially empty
- The printer produces a series of strings
- The machine enumerates (i.e., it lists out/prints) the strings in a language
- It may halt or loop
- The language may be infinite (the printer might print forever)
- It may print out duplicates
- It may print in any order

> A language is Turing-recognisable if some enumerator enumerates it.

Proof: (proof of construction)
1. Given an Enumerator "E" construct a TM "M"
   - On input w, M does the following steps:
     - Run "E"
     - Compare each output string to w
     - if we find a match, accept.
2. Given a TM "M", construct "E"
   - Construct E, using M as a subroutine
   - Run M on all possible strings
   - If M ever accepts a string, then print it out
   - But the problem is that M might loop on some particular strings
     - So we have to run all the strings in parallel
     - For i = 1, 2, 3, ... (infinite loop)
       - For j = 1 to i
         - Simulate M
           - Use sj as input (sj being the jth string on the list of all possible strings)
           - Run simulation for i steps
         - If M accepts sj (within i steps)
           - Then print sj
         - END
       - END
     - Note that this way all possible (i,j) values are addressed

## Formal definition of an Enumerator
An enumerator is a 7-tuple <Q, Σ, Γ, δ, q0, q_print, q_halt>
- Q = the set of states (finite)
- Γ = the work tape alphabet
- Σ = the output/print tape alphabet
- δ: Q x Γ -> Q x Γ x {L, R} x (Σ U ε) = the transition function
- q0 ε Q = the start state
- q_print ε Q = the print state
- q_halt ε Q = the halt state (q_print != q_halt)

The computation of an enumerator:
<br> Defined as an ordinary TM, except for following three points.
1. It has two tapes:
   - Work tape
   - Print tape
   - Both are initially blank.
2. At each step, the machine may write a symbol from Σ on the output tape, or nothing, as determined by δ
3. Whenever state q_print is entered, the output tape is reset to blank and the head returns to the left end and the output is printed. When q_halt is entered the machien will halt.

The Enumerated Language:
- The language enumerated by Enumerator is the collection of all the strings that Enumerator eventually prints out.
- Enumerator may generate the strings of the language in any order, possibly with repetitions.
- L(E) {w ε Σ* | w appears on the work tape if q_print is entered}

# Church-Turing Thesis
> "Algorithmically Computable" == "Computable by a TM"

# Encoding
Before we start, let's keep in mind that Turing Machines capture all algorithms. (Church-Turing Thesis)

Let's standardise the way we describe TM algorithms.<br>
What is the right level of detail to give when describing such algorithms?

We have three possibilities:
- Formal description of TM (spells out the TM's states, transition functions, etc)
- Implementation description (the description of the way that the TM moves its head and the way that it stores data on the tape, using natural languauge)
  - We do not give details of states or transition functions
- High-level description (the description of an algorithm using natural language, ignoring the implementation details)
  - We do not give details on how the machine manages its tape or head

# Decidable Languages
## Decidability
- Every question is about regular languages is decidable
- Some questions about CFLs are decidable, but some are not
- The "halting problem" is not decidable
- Some languages are not Turing recognisable
- Many questions about TM are not decidable, and some are not even Turing recognisable

### The Halting Problem
Given a program, will it halt?

Given a TM, will it halt when run on some particular given input string?

Given some program written in [Java/C/any other language], will it ever get into an infinite loop? Or will it always terminate?

Answer:
<br> In general, we can't always know.
- The best we can do is run the program and see whether it halts
- but for many programs, we can prove that "it will always halt" (or "it may sometimes loop").
- But for programs in general, the question is undecidable.

### Decidable Problems
1. Given a DFA and a string, will the DFA accept?
   - This problem is decidable because DFA either accepts or rejects.
   - Languages are decidable. We must express the problem in terms of languages
     - The input for this problem is a particular DFA and a string.
     - We can encode this into a language, say X.
     - "X is a member of the language iff the answer to the problem is yes."
   - Theorem:
     - The language A = {<B,w> | B is a DFA that accepts string w} is decidable.
     - Note that A is not regular or context-free, but is decidable
   - Proof:
     - Provide a TM that decides it.
       - The TM is given as input <B,w>: a DFA B and a string w, encoded into a string
       - The TM checks to make sure B is a valid representation of a DFA.
       - The TM then simulates B on w
       - If B reaches a final state at the end of w, then the TM will accept.
       - Otherwise, the TM will reject
     - This TM will always halt.
   - From the next question, the questions are given in the theorem form.
2. The language A = {<B,w> | B is a NFA that accepts string w} is decidable.
   - Proof:
     - Construct a TM that takes as input the representation of an NFA(B) and a candidate string(w).
     - Approach 1: simulate the NFA on w
     - Approach 2: convert the NFA to a DFA, and use the proof used in problem 1.
3. The language A = {<R,w> | R is a regular expression that generates string w} is decidable.
   - Proof:
     - We can build a TM that, given a RegEx R and string w as input, will determine whether <R,w> is in A.
     - and that algorithm/TM will always halt.

Note that often times we have to prove that an algorithm/TM always halts.
- Many programs can be proven to always halt
  - But this does not mean the HALTING PROBLEM is decidable

### More Decidable Problems for DFAs
1. Is string w in the language? | A = {<B,w> | ...}
2. Is the language empty? (L = ∅) | E = {<B\> | ...}
3. Are two languages the same? | EQ = {<A,B> | ...}

**Emptiness problem**<br>
The language E = {<A\> | A is a DFA and L(A) = ∅} is decidable.
- Algorithm/TM to decide it:
  - Given a DFA A, can we go from the initial state to a final state?
    - If so, then the DFA could generate some string
  - Is any final state reachable from the initial state?
    - A graph problem:
      - Mark the initial state
      - Repeat until no new states get marked
        - Mark any state where there is a transition to it from a marked state
      - Check to see if any final state got marked

**Equivalence problem**<br>
The language EQ = {<A,B> | A and B are DFAs and L(A) = L(B)} is decidable
- Proof;
  - Let C be the "symmetric difference" between A and B
    - C = anything in A or B but not both (XOR)
    - C = (A ∩ B^c) U (A^c ∩ B)
    - Note that if A=B then C = ∅
  - Given two or more DFAs, we know how to modify DFAs
    - complement
    - intersection
    - union
  - Build DFA C to accept the symmetric difference
  - Use the TM from previous theorem (emptiness problem) to test if C is empty. (Accept if so, Reject otherwise)

### More Decidable Problems for Context-Free Languages
1. Given a CFG, will it generate a given string w?
2. Given a CFG, is the language it generates empty?
3. Given two CFGs, do they accept the same language? (not decidable)

- Undecidable problems for CFL
  - Is a CFG ambiguous?
  - Do two CFG's have any strings they generate in common?
  - Is the complement of a CFG also a CFG?


**Acceptance problem**<br>
The language A = {<G,w> | G is a CFG that generates string w} is decidable
- All grammars are "parsable"
- Proof:
  - Idea 1: enumerate all leftmost derivations. For each, test to see if it generates w
    - Problem: if w is not in the language, then it may not halt
  - Idea 2: use Chomsky normal form
    - Inputs: G = a CFG, w = a string
    - Convert G into Chomsky normal form
      - Note that every derivation has exactly 2N-1 steps
        - one run for getting the derivation of length N
        - another run for converting it to terminals
    - List all derivations of length 2N-1
      - check each derivation to see if it generates w
      - if it does, accept. Otherwise, reject

**Emptiness problem**<br>
The language E = {<G\> | G is a CFG and L(G) = ∅} is decidable
- Check if S can generate a string of terminals
  - Mark variables that generate a string of terminals
  - If some variable generate a string of marked variables, mark it too
  - Repeat until no more variables can be marked
  - If S can generate a string of terminals, then the language is not empty. Otherwise, it is empty.
- This can also be put in algorithms
  - Repeat:
    - Look for a rule A -> XXX where all symbols on the right side has been marked
    - Mark the variable on the left side
  - until nothing more can be marked
  - If the start symbol is not marked (i.e., language is empty), accept. Otherwise reject
