# Lecture 2

---

## Choosing Breakpoint Example
Let 0 = g1 < g2 < ... < gp = L denote the campsites chosen by greedy <br>
Let 0 = f1 < f2 < ... < fq = L denote the campsites in an optimal solution

### 1. Proof by Induction: Greedy stays ahead
Lemma:<BR>
For all r: fr <= gr, with g for Greedy campsites and f for some optimal solution

Proof by induction:
- Base case (r = 1): When r = 1, g1 is as far away as possible, i.e. f1 <= g1
- Induction hypothesis: Suppose that for some k it holds that fk <= gk
- Induction step: 
  - To prove: for k + 1 it holds that f_(k+1) <= g_(k+1)
  - We know that fk <= gk by the IH.
  - Greedy selects g_(k+1) to be the campsite within reach as far from gk as possible
  - Campsite f(k+1) cannot be further than the farthest reachable from fk, and this is definitely within reach from gk because of the IH.
  - So f_(k+1) <= g(k+1)

### 2. Proof by Contradiction
Theorem: the greedy algorithm is optimal.

Proof by contradiction:
- Let k be the number of campsites selected by greedy, and m the number of campsites in an optimal solution f.
- Suppose Greedy is not optimal. so k > m and this gm < fm.
- However, fm <= gm with the Lemma from the previous proof
- Contradiction with gm < fm. So greedy must be optimal


## Interval scheduling
- Job (activity) j interval is given: starts at sj and finishes at fj
- Two jobs are compatible if they do not overlap
What is the maximum number of compatible intervals(jobs)?

### Proof by Induction:
Lemma
- For all r < k : f(ir) <= f(jr), with i denoting Greedy schedule and j some (optimal) one

Proof:
- Base case = (r = 1): Job i1 is chosen and thanks to order of jobs, f(ir) <= f(jr)
- Induction hypothesis: Suppose that for some k it holds that f(ik) <= f(jk)
- Induction step
  - To prove: for k+1 it holds that f(i(k+1)) <= f(j(k+1))
  - We know that f(jk) <= s(j(k+1)) as the jobs do not overlap.
  - So f(ik) <= s(j(k+1)) by the IH
  - So greedy can take j(k+1), but since Greedy chooses smallest end time, f(i(k+1)) < f(j(k+1))


### Proof by Contradiction:
Theorem:
- Greedy algorithm is optimal (i.e. has the most jobs)

Proof:
- Let k be the number of jobs selected by Greedy in i, and m the number of jobs in some optimal schedule j. Suppose Greedy is not optimal, that k < m.
- However, for all r <= k it holds that f(ir) <= f(jr) by Lemma from proof by induction.
- In particular: f(ik) <= f(jk)
- Thus there must be some job j(k+1) in optimal solution j which starts after jk, and thus after f(ik)
- But then after Greedy inserted ik, there was another compatible job
- This contradicts Greedy having only k jobs.


## Scheduling to minimising maximum lateness
Problem: Minimising lateness problem
- Single resource processes one job at a time
- Job j requires tj units of time and is due at dj
- If j starts at time sj then it finishes at fj = sj + tj
- Lateness of j is Lj = max(0, fj - dj). Maximum lateness = max(Lj)

The goal is to minimise the maximum lateness, i.e. minimise max(Lj).

The optimal ordering is the ascending order of deadlines
