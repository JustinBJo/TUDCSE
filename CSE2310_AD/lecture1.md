# Lecture 1. Greedy Algorithms

---

## 0. Today's content
- Checking ADS/R&L knowledge - algorithms with proofs
- An intro to greedy algorithms

- Prerequisite knowledge
  - Proving techniques: induction and contradiction
  - complexity analysis
  - data structures: stacks, queues, pqs, trees, graphs
  - graph algorithms
    - BFS, DFS, topological ordering
    - Dijkstra
    - Kruskal, prim-jarnik (minimum spanning trees)

## 1. Time complexity
- O(n) = Upper bound (T(n) is O(f(n)) iff there exists constant c and n0 larger than 0 such that n >= n0: T(n) <= c f(n))
- Ω(n) = Lower bound (T(n) >= c f(n))
- Θ(n) = Tight bound (T(n) is Θ(f(n)) iff T(n) is O(n) and T(n) is Ω(n))


- for all d > 0, log n is O(n^d)

## 2. Sorting
![img.png](img.png)

## 3. Graphs
- DAG
  - directed graph that contains no directed cycles (Directed Acyclic Graph)


- Topological ordering
  - A topological ordering of a directed graph G = (V,E) is and ordering of its nodes as v1, v2, ..., vn so that for every edge (vi, vj) we have i < j.
  - Every DAG has a topological ordering
  - Applications
    - Skill circuits (train skill x before y)
    - Compilation (run code x before y)
  - Algorithm: find a node with no incoming edges and place it before all the remainders


- If G is a DAG, then G has a topological ordering.
  - Prove that if G is a DAG, then G has a node with no incoming edges 
    - Proof by contradiction
        - Suppose that G is a DAG
        - Suppose every node has at least one incoming edge
        - Pick any node v and follow edges backwards from v
        - Repeat until we have gone back |V| times
        - We must now have visited a node twice
        - This means there is a cycle
        - There is a contradiction, so there must be no nodes with incoming edges.
  - Prove that if G is a DAG, then G has a topological ordering
    - Proof by induction
      - Base case: holds as for |V| = 1, because G already has a topological ordering
      - Induction hypothesis: If G is a DAG of size <= k, then G has a topological ordering
      - Induction steps:
        - Given a DAG G with k+1 nodes
        - Find a node v with no incoming vertices
        - G - {v} must be a DAG, as removing v cannot create cycles.
        - By the IH, G - {v} has a topological ordering T.
        - So v followed by T is a valid topological ordering for G as v has no incoming edges
      - Thus by induction we have proven the lemma

## 4. Proofs
1. Proof by induction
   - Greedy stays ahead
   - With equal number of stops, Greedy is at least as close to 