# Example multiple questions

#### Q1. Consensus algorithms (e.g. Paxos or Raft):
1. enable 2 nodes to decide on something 
2. work by replicating state machines 
3. are based on vector clocks 
4. enable a distributed system to agree on a common time

Answer: 2
1. They are crash fault-tolerant consensus with at least 2f+1 nodes with f faulty nodse
2. Consensus algorithms can be used in state-machine replication systems to keep to log module of replicated state machines in sync.
3. Consensus protocols:
   - Safety: all nodes are valid and return true
   - Availability: able to provide an answer if n/2 + 1 servers are operational
   - No clocks: they do not depend on RTCs to work
   - Immune to stranglers: if n/2 + 1 servers vote, then the result is considered safe.
4. Consensus: providing agreement in the presence of faulty nodes (no agreement on the sense of time)
   - Resource allocation
   - Committing a transaction
   - Synchronizing state machines
   - leader election
   - atomic broadcasts
   
#### Q2. A GFS chunkserver/HDFS datanode is responsible to:
1. Store filesystem path information
2. Split the data into partitions
3. Store data partitions
4. Replicate the data onto multiple disks

Answer: 3
1. Done by Master/NameNode
2. Done automatically
3. Chunkserver/datanode stores data chunks
4. Done automatically

#### Q3. Which of the following is the computation order of applying reduceL to a list of 10 integers with the ‘+’ operator?
Answer: 1 - (((((((((0 + 1) + 2) + 3) + 4) + 5) + 6) + 7) + 8) + 9)

#### Q4. We need to calculate the average temperature of the last 10 minutes every 30 minutes from a stream of measurements taken every minute. What type of window do we need to use?
1. Sliding window
2. Tumbling window
3. Jumping window
4. Session window

Answer: 3
- Jumping window has fixed time intervals, which corresponds to 30 minutes
- Windows could have size of 10 minutes

#### Q5. We have the following datasets:
- A => All the cars currently traveling through an intersection
- B => All the cars that have been parked in a garage for the last 3 months

1. Both datasets are unbounded data sets
2. Both datasets are bounded data sets
3. A is an unbounded data set and B is a bounded data set
4. A is a bounded data set and B is an unbounded data set

Answer: 3
- Bounded data: dataset that can be enumerated and/or iterated upon
- Unbounded data: dataset that we can only enumerate given a snapshot. Unbounded data does not have a size property
- Most datasets are unbounded.
- We need to have a snapshot of the cars passing through the intersection in order to count them, so they are unbounded.
- We don't need a snapshot for stationary cars, so they are bounded.

#### Q6. What kind of stream will be produced by the following Flink code snippet:
```dataStream.map(c => (c.id, 1)).keyBy(x => x._1).sum(1)```

Answer: 1 - Stream of the sums per ID

#### Q7. Which of the following best describes synchronous replication?
1. The master reports success after its cache has been flushed.
2. The master reports success after a configurable number of slaves have confirmed writes.
3. The master reports success after a write was committed to its own disk.
4. The master reports success after a read operation on its own disk results in the same outcome as a read operation on the disk of any of the slaves.

Answer: 2
- In synchronous replication, leader has to report success after a number of followers confirm.
- This makes synchronous replication system consistent, but less available.

#### Q8. Which of the following is true about Lamport timestamps and vector clocks?
1. Lamport timestamps and vector clocks both maintain total causal orders
2. To use Lamport timestamps or vector clocks, each node in a system needs to maintain a vector of size N, where N is the total number of nodes in the system
3. They both guarantee that if LP/VC(a) < LP/VC(b) for event a and b, then a must happen before b
4. Both guarantee that messages will arrive in order

Answer: all wrong (this question was removed)
1. they only keep partial orders
2. for LT, each node only need a single counter
3. for LT, it is true that if a->b then LT(a)<LT(b) but not the other way around (events may be unrelated). For VC it is symmetric.
4. no, because they only keep partial orders

#### Q9. What is the correct function signature for leftOuterJoin on Spark RDDs?
Answer: 4 - ```RDD[(K,V)].leftOuterJoin(other: RDD[(K, W)]): RDD[(K, (V, Option[W]))]```

#### Q10. Which of the following function(s) is/are higher order?
- A(a:Z,b:X)→X
- B(a:[T],x:T→V)→[V]
- C(a:T,f:V)→T

1. Only A 
2. A and B 
3. A and C 
4. Only B

Answer: 4
- A higher-order function is a function that takes another function as one of its arguments.

#### Q11. Which higher order function does the following signature correspond to?
```(xs:[A],f:(A,B)→B,acc:B):B```

Answer: 3 - foldR

#### Q12. Which of the following statements about Watermarks in stream processing systems is not correct.
1. The timestamp of the watermark signifies that all events carrying a timestamp up to the watermark timestamp should have arrived. 
2. Watermarks allow events that are out of order to be processed as long as the event arrives before the first watermark that has a later event-time than the event itself. 
3. A watermark can trigger multiple tumbling windows at once. 
4. The session gaps for session windows do not depend on what watermarks are used.

Answer: 2
1. correct definition of watermark
2. Watermarks allow late messages to be processed up to a specified amount of (event-time) delay (allowed lateness).
3. true
4. session gaps are independent of watermarks

#### Q13. Given that t is the timestamp an event is processed by a stream processor, event time skew is:
1. t−s, where s is the timestamp of the latest event processed.
2. t−s, where s is the timestamp when the last window trigger was fired. 
3. t−s, where s is the timestamp of the first event processed. 
4. t−s, where s is the timestamp of the actual timestamp of an event.

Answer: 1
- Event time skew is calculated t-s, where t is the processing time and s is the timestamp of the latest event processed
- Lag is calculated t-s, where t is the processing time and s is the actual timestamp of an event

#### Q14. Which of the following is not a replication architecture:
1. Master - Master 
2. Leaderless 
3. Master - Slave 
4. Eventually consistent

Answer: 4
- 1 to 3 are replication architectures.
- 4 is a consistency model in distributed database.

#### Q15. Which of the following statements is false? In the context of Big Data Processing, ETL pipelines:
1. Usually feed machine learning systems
2. Consume most of the developer/analyst project time
3. It is the job of managers and CEOs to design, code and execute them
4. Require special systems due to high volumes of data

Answer: 3
- ETL cycle is the cycle of processing big data
- Extract - Transform - Load
- Big data engineering is about building pipeline
- Big data analysis is about discovering patterns

#### Q16. Which of the following methods is part of the Observer interface, for dealing with push-based data consumption?
1. def subscribe(obs: Observer[A]): Unit
2. def onNext(a: A): Unit
3. def map(f: (A) -> B): [B]
4. def onExit(): Unit

Answer: 2
- Two fundamental technique for the client to process all available data in the data source:
  - Iteration: the client asks the data source if there are more items and pull next item
  - Observation: the data source pushes the next available item to a client end point
- Observer interface (for consumer):
```
trait Observer[A] {
    def onNext(a: A): Unit
    def onError(t: Throwable): Unit
    def onComplete(): Unit
```
- Observable interface (for producer):
```
trait Observable[A] {
    def subscribe(obs: Observer[A]): Unit
```

#### Q17. A transformation in Spark:
1. Schedules a pipeline run
2. Runs a pipeline and reports a result
3. Triggers a data shuffle
4. Does nothing

Answer: 1
1. transformations are lazy: they are only executed when there is an action
2. this is for action
3. data shuffling is performed when wide dependency transformations (groupByKey, join etc) are done
4. .

#### Q18. What is Byzantine fault tolerance?
1. Resilience against multiple node failures
2. Resilience against node failures when electing cluster leaders
3. Resilience against suboptimal voting
4. A mechanism used by the Byzantine empire for the good of its people

Answer: 3
- Byzantine fault tolerance is resilience against malicious nodes that lead to suboptimal voting.

#### Q19. Consider a cluster of 5 machines running HDFS (1 namenode, 4 datanodes). Each node in the cluster has a total of 1TB hard disk space and 128GB of main memory available. The cluster uses a block-size of 64 MB and a replication factor of 3. The master maintains 100 bytes of metadata for each 64MB block. Imagine that we upload a 128GB file. How much data does each datanode store?
1. 32GB
2. 64GB
3. 96GB
4. 128GB

Answer: 3

#### Q20. Which of the following statements is not true? An operating system kernel:
1. Provides a unified interface to hardware devices
2. Is the main library loaded when the computer starts
3. Contains and runs device drivers
4. Splits the computer resources to multiple users

Answer: 2
- The kernel is a computer program at the core of a computer's operating system and generally has complete control over everything in the system.

#### Q21. When multiple senders/receivers are involved, we need external ordering scheme. Which type of order is dependent on “happens before” relationships?
1. Reflexive order
2. Total order
3. Causal order
4. Asymptotic order

Answer: 3
1. Reflexivity is that an element is related to itself.
2. Total order is the absolute order of events
3. Causal order is the happens-before relation
4. --

#### Q22. Which of the following statements about microbatching (in streaming systems) is correct?
1. Every event is processed as soon as it arrives
2. The engine buffers events before processing them further
3. Microbatching allows element-wise operations to be executed per event
4. Microbatching enables us to process batch data in a streaming fashion

Answer: 2
1. Micro-batching aggregates data in batches of processing-time duration
2. True, because it takes data in for a period of time and then aggregates them
3. This is for event-based streaming
4. Micro-batching is an approach to stream processing, not batch processing.

#### Q23. In the case of Spark, narrow dependencies:
1. Are expensive, as they require extensive data shuffles
2. Represent element-wise operations
3. Allow for recalculating parts of the RDD, if a node dies
4. Trigger computations

Answer: 2
1. Data shuffles are done for transformations with wide dependencies
2. map, filter, union etc are element-wise operations, which have narrow dependencies
3. RDD lineage is in charge of fault tolerance in Spark
4. RDD actions are in charge of triggering computations

#### Q24. What is the correct function signature for reduce on Spark RDDs?
Answer: 2 - ```RDD[A].reduce(f: (A,A) -> A)```

#### Q25. Vector clocks
1. enable us to establish partial causal ordering of events
2. require space O(n2) for n processes
3. given 2 events A and B, enable us to determine which one happened first
4. are a protocol for replicating time machines

Answer: 1
1. Vector clocks do not establish full causal ordering because they can establish relation for non-related events
2. Vector clocks require O(n) timestamps to be exchanged
3. It does but only partially; same reason for 1
4. It is a protocol for ordering events.

#### Q26. Choose the correct implementation of the Monad interface in Scala:
Answer: 1
```
trait Monad[M[_]] {
   def unit[S](a: S) : M[S]
   def flatMap[S, T] (m: M[S], f: S => M[T]) : Monad[T]
}
```
Monads are design patterns that defines how functions can be used together to build generic types.<br>
In other words, Monad is a generic concept which helps in doing operations between pure functions to deal with side effects.<br>

#### Q27. An (in-memory) immutable data structure:
1. Updates values in place when updates are requested by the client
2. Can be safely shared across multiple machines
3. Can be safely shared across multiple threads
4. None of the above

Answer: 3
1. In data processing, we never modify data in place; instead we apply operations that create new versions of the data
2. ?
3. Immutable data helps in avoiding locking so we can process items in parallel.
4. --

#### Q28. What is eventual consistency?
1. At any time, the system is linearisable
2. At any time, concurrent reads from any node return the same values
3. If writes stop, all reads will return the same value after a while
4. If writes stop, a distributed system will become consistent

Answer: 3
1. This is linearizable consistency
2. This is linearizable consistency
3. Eventual consistency model ensures that all replicas reach a consistent state if no more user updates arrive
4. ?

#### Q29. Immutability enables us to:
1. Modify data with multiple threads
2. Create classes that do not change
3. Provide safe access to shared data in memory
4. All the above

Answer: 3
1. Immutability is there to avoid the modification of data across multiple threads
2. Immutability is for data, not class
3. Immutability maintains the old versions of data, so the data can be kept.
4. --

#### Q30. Which higher order function does the following code snippet correspond to:
```
  def f[A](xs: List[A], ys: List[B]) : List[(A, B)] = (xs, ys) match {
    case (_, Nil) => Nil
    case (Nil, _) => Nil
    case (a :: xss, b :: yss) => (a, b) :: f(xss, yss)
  }
```
Answer: 4 - zip

#### Q31. Given the following value in Scala: <br> ```val statement = List(List("some", "questions"), List("are", "difficult"))``` <br> which of the following sequences of function calls would converted it to the string: “some questions are difficult”
1. ```statement.flatMap(x => x).flatten```
2. ```statement.flatten.reduce((a, b) => a + " " + b)```
3. ```statement.foldLeft(List[String]())((x : List[String], y : List[String]) => x ::: y)```
4. ```statement.reduceByValue(_ + _)```

Answer: 2
1. This would give List(s, o, m, e, q, u, e, s, t, i, o, n, s, a, r, e, d, i, f, f, i, c, u, l, t)
   - flatMap operation on a list of strings would flatten the string into characters
2. This would be the same as List("some", "questions", "are", "difficult").reduce, which would be what we need
3. This would give List("some", "questions", "are", "difficult")
4. This would throw an error because we cannot perform + on lists

#### Q32. What does Amdahl’s law prescribe?
Not a part of this course

#### Q33. Multi-leader systems have issues with write conflicts. Which of the following is the most plausible way of resolving them?
1. Maintain a write lock. Only one client at any moment can acquire it.
2. Use Lamport timestamps: this will help determine the order of incoming writes.
3. Report conflicts to clients and let clients handle them.
4. Move conflicting writes to another cluster leader.

Answer: 1
1. This allows only one client can write at a time, so no write conflicts will happen.
2. Lamport timestamps cannot determine total order
3. This could be a solution, but not very plausible
4. Not a plausible solution

#### Q34. A Unix pipe (denoted by |) enables us to:
1. Move text from the input of a command to the output of another command
2. Copy data from one location on the hard drive to another
3. Move structured records between two commands
4. Move unstructured data between two commands

Answer:4
1. Pipes forward a program's output to input of another program.
2. --
3. Unix processes with unstructured data
4. correct

#### Q35. Which of the following statements are true?
- The C in ACID and CAP mean the same thing
- Big data engineering is concerned with building pipelines, while big data analytics is concerned with discovering patterns, so we could say that big data analytics is the same as machine learning (ML), which also involves discovering patterns

1. Only a is true 
2. Only b is true 
3. Both are true 
4. Both are false

Answer: 4
- ACID: atomicity, consistency, isolation, durability / CAP: consistency, availability, partition tolerance
- Big data engineering: building pipelines / big data analysis: discovering patterns

#### Q36. Given that file.txt is a two column CSV file, what does the following Unix command do?

```$ sed -e 's/^\(.*\),\(.*\)$/\2 \1/' < file.txt | sort```

1. Changes the order of columns in a 2 column file, then sorts by column 1
2. Concatenates columns 1 and 2, then sorts by column 2
3. Removes columns 1 and 2, then sort by whatever remains
4. Appends columns 1 and 2 to file.txt and then sorts it

Answer: 1
- sed modifies a string at its input in various ways using pattern matching, such as removing or changing order
- sort writes a lexicographical sorted concatenation of all input files to STDOUT.

#### Q37. For our new budget-constrained startup, called DelayedGram, we are building an application that serves millions of cat videos to millions of users in parallel. Which architecture would be more suitable?
1. A queue that stores and forwards a user request to a centralized database, which also contains the videos 
2. A web server that serves videos using a cloud-based object store (e.g. Amazon S3)
3. A stream processor that registers the request and starts streaming video bytes to the user 
4. An in-memory cache that holds all videos, served by a web server

Answer: 2
- Directly serving videos would be expensive

#### Q38. Why do Spark RDDs contain lineage information?
1. To enable fault tolerance
2. To increase parallelism 
3. To deal with issues in data partitioning 
4. To enable distributed snapshots

Answer: 1
- RDDs contain information on how to compute themselves and their dependencies to other RDDs
- Lineage information allow an RDD to be traced to its ancestors.
- Spark uses RDD lineage information to know which partitions to recompute in case of a node failure.

#### Q39. Which one of the following statements is true, in the context of Unix?
1. awk enables reduce-like operations 
2. sed enables reduce-like operations 
3. xargs enables reduce-like operations 
4. ls enables reduce-like operations

Answer: 1
1. awk - scans a file line by line and can split each line into fields. It can also perform actions on the fields, which enables reduce-like operations.
2. sed - modifies strings using pattern matching
3. xargs - equivalent to map
4. ls - lists all files in current directory

#### Q40. Which of the following RDD API calls is a performance killer in Spark?
1. reduceByKey
2. keyBy
3. groupByKey
4. aggregateByKey

Answer: 3
- reduceByKey/aggregateByKey vs groupByKey
  - reduceByKey/aggregateByKey: before shuffling, all the pairs with the same key on the same machine are combined
  - groupByKey transfers all data over the network, including unnecessary data
  - shuffling stage for reduceByKey or aggregateByKey is minimal or none because reduction happens locally 
- keyBy has a narrow dependency
