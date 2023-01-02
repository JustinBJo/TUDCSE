# Lecture 3 20221123

---

## MST and cut property
Spanning Tree
- A spanning tree T of a graph G = (V,E) is a subset of edges T, such that the graph G' = (V,T) is strongly connected.

Minimum Spanning Tree
- A MST of a graph G = (V,E) is spanning tree T, such that the cost c(T) = Σ(e in T)(w(e)) is minimal.
- That is, there is no spanning tree T', such that c(T') < C(T).

Cut property
- Let S be any subset of nodes V, and let e be the min cost edge with exactly one endpoint in S (i.e., the cutset).
- Then there is an MST T that contains e.

- Proof
  - Let T be an MST. If e is in T we're done.
  - If not,
    - Adding e to T must create some cycle.
    - Therefore there is another edge f(!= e) that connect S to V-S
    - But w(e) <= w(f), so (T - {f}) U {e} has a cost that is no larger and is also still a spanning tree.
    - Thus we have now an MST that contains e.

## Prim-Jarnik
1. Take one node and add to T
2. Find an edge that connects a vertex in T and not in T with the minimum weight
3. Add the vertex that is not in T (and the edge)
4. Repeat 2 and 3 until all the vertices are in T.

Runtime: same as Dijkstra's
- Θ((|V|+|E|)log|V|) when we use a priority queue, which is
- Θ(|E|log|V|) for connected graphs

## Cycle Property
Let C be any cycle in G, and let e be the max cost edge in C. Then e is not in any MST T.

Proof.
- For the sake of contradiction, let T be an MST of the graph such that e={u,v} in T.
- Remove e from the graph. This breaks it into two parts V1 and V2 that are not connected, with u in V1 and v in V2.
- But since C was a cycle, there must be an edge f to connect V1 and V2.
- And w(f) < w(e) (by choice of e), so add f to T.
- Now for T' = (T - {e}) U {f} : c(T') < c(T), so T can't be and MST.
- Contradiction, so e cannot be in any MST.

## Kruskal
1. Sort edges in ascending order of weights
2. Take in edges unless they create cycles
3. Repeat until there are |V|-1 edges.

Detecting cycles:
1. Id-based detection
   - Every node starts with their own id as their 'cycle id'
   - If we put two nodes together (i.e., add an edge between them), this is only allowed if their cycle ids are different.
   - We then update both ids to be the maximum of the two ids.
   - But this becomes very inefficient if we update the whole cycle every time (O(|V|) time to add every edge)
2. Union-Find
   - Track elements partitioned into disjoint subsets
   - Union method and Find method

## Union-Find
Runtime
- Union-Find allows m union/find operations on n sets in O(mlogn) time.
- For Kruskal we have |V| sets, on which we do at most |E| union/find operations
- Furthermore sorting the edges is Θ(|E|log|E|)
- So the runtime is Θ(|E|log|E|) = Θ(|E|log|V|) time.


---

## Clustering
k-Clustering
- Divide objects into k non-empty groups
- Spacing: minimum distance between any pair of points in different clusters
- Problem: given an integer k, find a k-clustering of maximum spacing

How can we efficiently divide objects into k non-empty groups such that the minimal distance between groups (spacing) is maximised?
- Grow an MST (with Kruskal) and stop after n-k edges
1. Form graph (without edges) on vertex set
   - This corresponds to n initial clusters
2. Find the closest pair of objects from different clusters
3. Add edge between them
4. Repeat n-k times until there are exactly k clusters left

Theorem
- Let C* denote the clustering C*1, ..., C*k formed by deleting the k-1 most expensive edges of a MST by Kruskal. C* is a clustering of maximum spacing.

Proof.
- The spacing of C* is the length d* of the (k-1)th most expensive edge
- Let C denote some other arbitrary clustering C1, ..., Ck
- Let p,q be in the same cluster in C*, say C*r, but in different clusters in C, say Cs and Ct.
- Some edge (p', q') on the p-q path in C*r spans two different clusters in C
- All edges on this path have length <= d* since Kruskal chose them.
- So spacing of C is <= d*, since p' and q' are in different clusters
- Since C is arbitrary, this holds for all C.