# Recognisable Languages

---

# 1. Turing Machines

## Introduction to Turing Machines
After the FSM and PDA, the Turing Machine is a new model of computation. It addresses:
- Decidable languages
- Turing recognisable languages
- Languages that are not Turing recognisable

Let's revise the "Language onion"
- All languages (some are not Turing recognisable)
- contains Turing recognisable languages
- contains Decidable languages
- contains Context-free languages
- contains Regular languages

So what does a Turing machine do?
- The data structure
  - for FSM was only the input string
  - for PDA was the input string and a stack
  - for TM is a "tape"

The tape
- The tape is a sequence of cells, where each cell contains a tape alphabet
- The tape has infinite length
- We have a tape head, which is the current position (initially the first cell)
- We can move the tape head to the right or left by one step
- We can scan/update the cell that the head is pointing
- Tape alphabet
  - Typically, we have Σ = {0, 1}
  - Also commonly we have Σ = {0, 1, a, b, x, #, $}
  - The blank symbol is special; it is not in the input alphabet
  - The input string is on the tape, and the blank symbol is used to fill the infinite tape

### Rules of Operation
At each step of the computation:
- read the current symbol
- update the same cell
- move one cell to either left or right
  - we do not stay in the same cell
  - unless we are at the leftmost cell and trying to move left
- The notation looks like below:
  - ```
       a -> b, R
    o ------------> o
    ```
  - a is the symbol to read
  - b is the symbol to write (can be the same as read symbol)
  - R is the direction to move ("L" or "R")

Ending computation:
- We have an initial state and final states (accepting/rejecting)
- Computation can end in three ways:
  - Halt and Accept
    - Whenever the machine enters the accept state, computation immediately halts
  - Halt and Reject
    - Whenever the machine enters the reject state, computation immediately halts
  - Loop
    - The machine fails to halt
- The TM is deterministic

## Formal definition of Turing Machine
> M = (Q, Σ, Γ, δ, q0, q_accept, q_reject)
> - Q = set of states
> - Σ = input alphabets
> - Γ = tape alphabets
>   - Σ is a subset of Γ
> - q0 = initial state
> - q_accept, q_reject, q0 ε Q
> - δ = Q x Γ -> Q x Γ x {L, R}

### Configuration
Configuration gives the entire state of the machine.
<br>It is a snapshot of execution at some step.

We need:
- contents of the tape
- location of the tape head
- current state

We can represent the entire history of the computation by a sequence of configurations
- starting with the start configuration
- ending with an accepting configuration
- and containing only legal transitions, provides a computation history

## TM related languages
### Decidable languages
> A Turing machine will always halt (accept or reject) for decidable languages.

### Turing recognisable languages
> When given a string that is in the language, Turing machine will always halt and accept for Turing recognisable languages. <br>
> For a string that is not in the language, Turing machine will either halt and reject or loop.

### Not Turing recognisable languages
> Languages that cannot construct a TM that recognises them.


## TM programming techniques
How can we recognise the left end of the tape?
- want to put a special symbol $ on the left end and shift the input over 1 cell to the right

Subroutines
- We can use several simpler TMs to form a complex one

Marking symbols
- We can mark symbols with dots to "remember the location".


# 2. Variants of Turing Machines
## Multi-tape TM
> Every multi-tape TM has an equivalent single-tape TM.

Multitape TM's have k tapes. In each transition, we have k top tape symbols, k push tape symbols, and k directions.

### How to build a single-tape TM from a multitape TM
What we need to achieve:
- store all tapes on a single tape
- each tape has a tape head
- need to transform a move in the multitape TM into one or more moves in the single-tape TM

How to address them:
- separate the tapes with a special symbol to indicate the start/end of a tape.
- add "dots" to show where head "k" is.
- for each transition in multitape TM,
  - scan for head of tape k and pop/push accordingly for k tapes
  - scan again and move the dots accordingly for k tapes
  - whenever one head moves off the right end, we must shift our tape so we can insert a blank.

## Nondeterministic TM
> At each moment in the computation, there can be more than one successor configuration

The main difference between a normal (deterministic) TM and a nondeterministic TM is the transition functions:
- δ: Q x Γ -> P(Q x Γ x {L, R})
- for a given state and the tape head alphabet, we can have different choices of transitions

Before, we had a linear configuration for an input string. With nondeterministic TM, we have a tree of configuration,
because at each state and tape head we can have number of states we can go to.

Some branches in the configuration tree can reach the accept state and halt. Some branches may reach reject and halt.
Some branches may never halt.

If any branch of the computation accepts, then the nondeterministic TM will accept.<Br>
If all branches of the computation rejects, (and all branches actually halts,) then the TM will reject.
If no branch gives accept and some branch never halts, then the TM loops.

### Equivalence of Nondeterministic TM and deterministic TM
Given a nondeterministic TM(N), show how to construct an equivalent deterministic TM(D).
- If N accepts (on any branch) then D will accept
- If N halts on every branch without any accepts, the D will halt and reject
- Approach: 
  - simulate N; 
  - simulate all branches of computation; 
  - search for any way N can accept

Searching for an accepting branch:
- Number each branch in the tree, so that the accepting node can be found with a combination of numbers
- Perform a breadth-first search (because some branches might go on forever)

Simulating N with D using Multitape TM:
- Use 3 tapes:
  - input tape: initial input; never modified
  - simulation tape: used like the tape of a deterministic TM to perform the simulation
  - address tape: used to control the breadth-first search; tells which choices to make during a simulation

The address:
- We have the maximum number of branches at any node for the configuration tree. Say this number is m.
- We have an address list, which is a list of addresses that can be taken in a configuration tree in a breadth-first order.
- Whenever m is encountered, we go down to the next level.

The algorithm:<br>
Initially, tape 1 contains the input and other tapes are empty.
1. Copy tape 1 to tape 2
2. Consider the next address by copying the next address on the address list to tape 3.
3. Run the simulation using tape 2 as "the tape"
4. When choices occur, look at tape 3 to find which branch to follow.
5. If at the end the branch rejects or dies out, or if the node does not exist, then abort this branch and go back to step 1
6. If accept is ever encountered, halt and accept. If all branches reject or die out, then halt and reject.

### 
A language if Turing Recognisable iff some non-deterministic TM recognises it.
- Halting - if a nondeterministic TM halts on all branches without accepting, then it rejects.

A language is decidable iff some non-deterministic TM decides it.
- Deciding means
  - will always halt
  - will always accept or reject
  - will never loop