# Programming for Big Data

---

## 1. Basic Data Types
- Unstructured: data whose format is not known (raw txt, html)
- Semi-Structured: data with a known format (json, csv, xml)
- Structured: data with known formats, linked together in graphs or tables (SQL or Graph DBs)

### Sequences/Lists
> Represent consecutive items in memory
- Size bounded by memory
- Items can be accessed by an index
- Items can only be appended
- Can be sorted

### Sets
> Store values without any particular values without duplicates
- Size bounded
- Can be queried
- Operations: union, intersection, difference, subset

### Maps or dictionaries
> Collection of (k,v) pairs in sucha way that each k appears only once
- One key always corresponds to one value
- Accessing a value given a key is very fast (~= O(1))

### Nested data types: Graph
> Set of vertices or nodes with a set of ordered or unordered pairs of these vertices
- Nodes contain attributes
- Edges can contain weights and directions
- Usually represented as Map[Node, List[Edge]]

### Nested data types: Trees
> Ordered graphs without loops

### Tuples
> An n-tuple is a sequence of n elements, whose types are known

### Relations
> Set of n-tuples of the same type; on of the tuple elements denote a key which are unique

### K/V pairs
> More general type of relations, where keys can be repeated


## 2. Functional Programming
1. No side-effects
2. Immutable data structures
3. Higher-order functions
4. Laziness

### Functions and signatures
- map(x: List[A], f: A->B): List[B]
- flatMap(x: List[A], f: A->List[B])): List[B]
- foldLeft(x: List[A], f: (B, A) -> B, init: B): B
- foldRight(x: List[A], f: (A, B) -> B, init: B): B
- reduce(x: List[A], f: (A, A) -> A): A
- groupBy(x: List[A], f: A -> K): Map[K, List[A]]
- filter(x: List[A], f: A->Boolean): List[A]
- scanL(x: List[A], f: (B,A) -> B, init: B): List[B]
- zip(x: List[A], y: List[B]): List[(A,B)]


- mapValues(kv: [(K,V)], f: V->U): [(K,U)]
- groupByKey(kv: [(K,V)]): [(K,[V])]
- reduceByKey(kv: [(K,V)], f:(V,V)->V): [(K,V)]
- join(kv1: [(K,V)], kv2: [(K,W)]): [(K, (V,W))]

### Monads
> A design pattern that defines how functions can be used together to build generic types.<br>
> A generic concept which helps in doing operations between pure functions to deal with side effects

```
trait Monad[M[_]] {
    def unit[S](a:S): M[S]
    def flatMap[S,T] (m:M[S])(f:S -> M[T]): M[T]
}
```

## 3. Enumerating datasets
In a big data system:
- Client code processes data
- A data source is a container of data

There are two fundamental techniques for the client to access the data source
- Iteration: the client asks the data source whether there are items left and then pulls the next item
- Observation: the data source pushes the next available item to a client

### Iteration
```
trait Iterator[A] {
    def hasNext: Boolean
    def next(): A
}
```

### Observation
```
// Consumer
trait Oberver[A] {
    def onNext(a: A): Unit
    def onError(t: Throwable): Unit
    def onComplete(): Unit
}

// Producer
trait Observable[A] {
    def subscribe(obs: Observer[A]): Unit
}
```

## 4. Copy-On-Write (COW)
> A general technique that allows us to share memory for read-only access across processes
> and deal with writes only if/when they are performed by copying the modified resource in a private version